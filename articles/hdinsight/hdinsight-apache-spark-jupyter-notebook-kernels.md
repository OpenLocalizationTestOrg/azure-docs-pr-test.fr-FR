---
title: les clusters aaaKernels pour bloc-notes jupyter sur Spark dans Azure HDInsight | Documents Microsoft
description: "Découvrez les noyaux hello PySpark, PySpark3 et Spark pour bloc-notes jupyter disponible avec les clusters de Spark sur Azure HDInsight."
keywords: bloc-notes jupyter sur spark,jupyter spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Noyaux pour bloc-notes Jupyter sur les clusters Spark dans Azure HDInsight 

Les clusters HDInsight Spark fournissent des noyaux que vous pouvez utiliser avec hello bloc-notes jupyter sur Spark pour tester vos applications. Un noyau est un programme qui exécute et interprète votre code. les trois noyaux Hello sont les suivantes :

- **PySpark** : pour les applications écrites en Python2
- **PySpark3** : pour les applications écrites en Python3
- **Spark** : pour les applications écrites en Scala

Dans cet article, vous apprendrez comment toouse ces avantages hello leur utilisation et noyaux.

## <a name="prerequisites"></a>Composants requis

* Un cluster Apache Spark dans HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Créer un bloc-notes Jupyter sur Spark HDInsight

1. À partir de hello [portail Azure](https://portal.azure.com/), ouvrez votre cluster.  Consultez [liste et afficher les clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) pour obtenir des instructions hello. cluster de Hello est ouvert dans un nouveau panneau de portail.

2. À partir de hello **liens rapides** , cliquez sur **tableaux de bord du Cluster** tooopen hello **tableaux de bord du Cluster** panneau.  Si vous ne voyez pas **liens rapides**, cliquez sur **vue d’ensemble** à partir du menu de gauche hello sur le panneau de hello.

    ![Bloc-notes Jupyter sur Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "Bloc-notes Jupyter sur Spark") 

3. Cliquez sur **Bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.
   
   > [!NOTE]
   > Vous pouvez également atteindre hello bloc-notes jupyter sur cluster Spark par hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. Cliquez sur **nouveau**, puis cliquez sur **Pyspark**, **PySpark3**, ou **Spark** toocreate un ordinateur portable. Utiliser le noyau de Spark hello pour les applications Scala, noyau PySpark pour les applications Python2 et PySpark3 noyau pour les applications Python3.
   
    ![Noyaux pour bloc-notes Jupyter sur Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "Noyaux pour bloc-notes Jupyter sur Spark") 

4. Un bloc-notes s’ouvre avec le noyau hello que vous avez sélectionné.

## <a name="benefits-of-using-hello-kernels"></a>Avantages de l’utilisation de noyaux de hello

Voici quelques avantages de l’utilisation de noyaux hello avec bloc-notes jupyter sur les clusters HDInsight de Spark.

- **Contextes prédéfinis**. Avec **PySpark**, **PySpark3**, ou hello **Spark** noyaux, vous n’avez pas besoin tooset hello Spark ou ruche contextes explicitement avant de commencer à utiliser avec vos applications. Ils sont disponibles par défaut. Ces contextes sont les suivants :
   
   * **sc** : pour le contexte Spark
   * **sqlContext** : pour le contexte Hive

    Par conséquent, vous n’avez pas hello suivant des contextes de hello tooset toorun instructions :

        sc = SparkContext('yarn-client')    sqlContext = HiveContext(sc)

    Au lieu de cela, vous pouvez utiliser directement hello présélection contextes dans votre application.

- **Commandes magiques de cellule**. Hello PySpark noyau fournit certaines prédéfinies « magics », qui sont des commandes spéciales que vous pouvez appeler avec `%%` (par exemple, `%%MAGIC` <args>). commande magic Hello doit être hello premier mot d’une cellule de code et de plusieurs lignes de contenu. word magique de Hello doit être hello premier mot de cellule de hello. Ajout de quoi que ce soit avant magic hello, même des commentaires, provoque une erreur.     Pour plus d’informations sur les commandes magiques, cliquez [ici](http://ipython.readthedocs.org/en/stable/interactive/magics.html).
   
    Hello tableau suivant répertorie les magics différents de hello disponibles via les noyaux hello.

   | Commande magique | Exemple | Description |
   | --- | --- | --- |
   | help |`%%help` |Génère une table de tous les magics disponibles hello avec exemple et la description |
   | info |`%%info` |Génère des informations de session pour le point de terminaison Livy actuel hello |
   | CONFIGURER |`%%configure -f`<br>`{"executorMemory": "1000M"`<br>`"executorCores": 4`} |Configure les paramètres hello pour la création d’une session. Hello indicateur force (-f) est obligatoire si une session a déjà été créée, ce qui garantit la session hello est supprimé et recréé. Consultez la section [POST /sessions Request Body de Livy](https://github.com/cloudera/livy#request-body) pour obtenir la liste des paramètres valides. Paramètres doivent être passées comme une chaîne JSON et doivent être sur la ligne suivante de hello après magique de hello, comme indiqué dans l’exemple, la colonne hello. |
   | sql |`%%sql -o <variable name>`<br> `SHOW TABLES` |Exécute une requête Hive sur hello sqlContext. Si hello `-o` paramètre est passé, résultat hello de requête de hello est conservée dans hello %% contexte Python local en tant qu’un [Pandas](http://pandas.pydata.org/) trame de données. |
   | local |`%%local`<br>`a=1` |Tout code hello dans les lignes suivantes est exécuté localement. Code doit être un code Python2 valide même indépendamment de noyau hello que vous utilisez. C’est le cas, même si vous avez sélectionné **PySpark3** ou **Spark** noyaux lors de la création d’ordinateur portable hello, si vous utilisez hello `%%local` magique dans une cellule, cette cellule doit seulement avoir un code Python2 valide... |
   | journaux |`%%logs` |Sorties hello des journaux de session de Livy hello en cours. |
   | delete |`%%delete -f -s <session number>` |Supprime une session spécifique de point de terminaison Livy actuel hello. Notez que vous ne peut pas supprimer la session de hello qui est initiée pour noyau hello lui-même. |
   | cleanup |`%%cleanup -f` |Supprime toutes les sessions de hello pour hello Livy point de terminaison actuel, y compris la session de cet ordinateur portable. indicateur de force Hello -f est obligatoire. |

   > [!NOTE]
   > En outre toohello magics ajouté par le noyau de PySpark hello, vous pouvez également utiliser hello [intégrés IPython magics](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics), y compris `%%sh`. Vous pouvez utiliser hello `%%sh` magique toorun scripts et bloc de code sur le nœud principal du cluster hello.
   >
   >
2. **Visualisation automatique**. Hello **Pyspark** noyau visualise automatiquement sortie hello de ruche et les requêtes SQL. Vous pouvez choisir entre plusieurs types de visualisations, notamment tableau, secteurs, courbes, aires et barres.

## <a name="parameters-supported-with-hello-sql-magic"></a>Paramètres pris en charge par hello %% magique de sql
Hello `%%sql` magique prend en charge des paramètres différents que vous pouvez utiliser le type de hello toocontrol de sortie que vous recevez lorsque vous exécutez des requêtes. Hello tableau suivant répertorie la sortie de hello.

| Paramètre | Exemple | Description |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |Utilisez le paramètre toopersist hello le résultat de requête de hello, Bonjour %% contexte local de Python, comme un [Pandas](http://pandas.pydata.org/) trame de données. nom de Hello de variable de trame de données hello est nom de variable hello que vous spécifiez. |
| -q |`-q` |Utilisez cette tooturn off visualisations pour la cellule de hello. Si vous ne souhaitez pas tooauto-visualiser le contenu d’une cellule hello et souhaitez toocapture sous la forme d’une trame de données, puis d’utiliser `-q -o <VARIABLE>`. Si vous souhaitez tooturn off visualisations sans capturer les résultats hello (par exemple, pour exécuter une requête SQL, comme un `CREATE TABLE` instruction), utilisez `-q` sans spécifier un `-o` argument. |
| -m |`-m <METHOD>` |**METHOD** prend la valeur **take** ou **sample** (**take** est la valeur par défaut). Si la méthode hello est **prendre**, noyau de hello récupère les éléments de haut hello hello résultats du jeu de données spécifié par le nombre maximal de lignes (décrite plus loin dans ce tableau). Si la méthode hello est **exemple**, éléments hello du jeu de données en fonction de trop échantillonne de noyau de hello`-r` paramètre décrit ci-après dans cette table. |
| -r |`-r <FRACTION>` |Ici, **FRACTION** est un nombre à virgule flottante compris entre 0,0 et 1,0. Si la méthode d’échantillonnage hello pour la requête SQL hello est `sample`, puis le noyau de hello échantillonne fraction spécifiée de hello d’éléments hello hello du jeu de résultats pour vous. Par exemple, si vous exécutez une requête SQL avec des arguments de hello `-m sample -r 0.01`, 1 % des lignes de résultat hello sont échantillonnées aléatoirement. |
| -n |`-n <MAXROWS>` |**MAXROWS** est une valeur entière. noyau de Hello limite le nombre de hello de lignes de sortie trop**MAXROWS**. Si **MAXROWS** est un nombre négatif comme **-1**, nombre de hello de lignes dans le jeu de résultats hello n’est pas limité. |

**Exemple :**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

instruction Hello ci-dessus hello suivant :

* Elle sélectionne tous les enregistrements présents dans **hivesampletable**.
* Comme nous utilisons le paramètre - q, elle désactive la visualisation automatique.
* Étant donné que nous utilisons `-m sample -r 0.1 -n 500` il échantillonne de 10 % des lignes hello dans hello hivesampletable et limites hello taille hello ensemble too500 de lignes de résultats.
* Enfin, étant donné que nous avons utilisé `-o query2` il enregistre également une sortie de hello dans une trame de données appelée **requête2**.

## <a name="considerations-while-using-hello-new-kernels"></a>Considérations lors de l’utilisation de noyaux hello

Quelle que soit la noyau que vous utilisez, en laissant les blocs-notes hello en cours d’exécution consomme des ressources de cluster hello.  Ces noyaux, car les contextes de hello sont prédéfinis, simplement en cours de fermeture blocs-notes de hello ne pas tuer le contexte de hello et par conséquent, les ressources de cluster hello continueront toobe en cours d’utilisation. Il est conseillé de toouse hello **fermer et s’arrêter** option à partir de l’ordinateur portable hello **fichier** menu lorsque vous avez terminé d’utiliser le bloc-notes hello, qui supprime le contexte de hello et puis se ferme hello bloc-notes.     

## <a name="show-me-some-examples"></a>Voici quelques exemples :

Lorsque vous ouvrez un bloc-notes jupyter, vous voyez deux dossiers disponibles au niveau racine de hello.

* Hello **PySpark** dossier a blocs-notes de l’exemple hello de cette utilisation new **Python** noyau.
* Hello **Scala** dossier a blocs-notes de l’exemple hello de cette utilisation new **Spark** noyau.

Vous pouvez ouvrir hello **00 - [lecture ME première] fonctionnalités de noyau Spark Magic** bloc-notes de hello **PySpark** ou **Spark** toolearn dossier sur magics différents de hello disponibles. Vous pouvez également utiliser hello autres blocs-notes exemple disponibles sous hello deux dossiers toolearn comment tooachieve différents scénarios à l’aide du bloc-notes portables avec les clusters HDInsight Spark.

## <a name="where-are-hello-notebooks-stored"></a>Où sont stockées les blocs-notes de hello ?

Notebook portables sont enregistrés toohello compte de stockage associé au cluster hello sous hello **/HdiNotebooks** dossier.  Ordinateurs portables, des fichiers texte et des dossiers que vous créez à partir de Notebook sont accessibles à partir du compte de stockage hello.  Par exemple, si vous utilisez Notebook toocreate un dossier **MonDossier** et un ordinateur portable **myfolder/mynotebook.ipynb**, vous pouvez accéder à cet ordinateur portable à `/HdiNotebooks/myfolder/mynotebook.ipynb` dans le compte de stockage hello.  Hello inverse est également vrai, autrement dit, si vous téléchargez un bloc-notes directement du compte de stockage de tooyour à `/HdiNotebooks/mynotebook1.ipynb`, portable de hello est également visible dans le bloc-notes.  Ordinateurs portables restent dans le compte de stockage hello même après la suppression de cluster de hello.

méthode Hello portables sont enregistrées de compte de stockage toohello est compatible avec HDFS. Par conséquent, si vous SSH en cluster hello que vous pouvez utiliser fichier de commandes de gestion comme indiqué dans hello suivant extrait de code :

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


En cas de problèmes d’accès du compte de stockage hello pour le cluster de hello, ordinateurs portables de hello sont également enregistrées sur le nœud principal de hello `/var/lib/jupyter`.

## <a name="supported-browser"></a>Navigateur pris en charge

Les blocs-notes Jupyter sur clusters Spark HDInsight sont pris en charge uniquement sur Google Chrome.

## <a name="feedback"></a>Commentaires
noyaux Hello sont en pleine évolution étape et arrivent au fil du temps. Les API pourront également être amenés à évoluer au fur et à mesure des évolutions des noyaux. Nous aimerions recevoir vos commentaires concernant l'utilisation de ces nouveaux noyaux. Cela est utile dans la mise en forme de la version finale de hello de ces noyaux. Vous pouvez laisser vos commentaires/commentaires sous hello **commentaires** section bas hello de cet article.

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
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)
