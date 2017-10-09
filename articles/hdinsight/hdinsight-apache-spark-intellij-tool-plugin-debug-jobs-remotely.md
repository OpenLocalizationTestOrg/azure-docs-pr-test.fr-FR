---
title: "aaaAzure boîte à outils pour IntelliJ - débogage des applications à distance sur HDInsight Spark | Documents Microsoft"
description: "Découvrez comment utiliser les outils HDInsight dans la boîte à outils Azure pour les applications de débogage tooremotely IntelliJ en cours d’exécution sur des clusters HDInsight Spark via vpn."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Utilisez la boîte à outils Azure pour les applications de toodebug IntelliJ à distance sur HDInsight Spark via VPN

Nous vous recommandons de façon hello du débogage applicaltion spark à distance via ssh. Pour obtenir des instructions, reportez-vous à la rubrique [Déboguer des applications Spark à distance sur un cluster HDInsight avec le kit de ressources Azure pour IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

Cet article fournit des instructions sur le toouse hello outils HDInsight dans la boîte à outils Azure pour IntelliJ toosubmit un travail Spark sur le cluster HDInsight Spark et déboguer à distance à partir de votre ordinateur de bureau. toodo par conséquent, vous devez effectuer hello suivant les étapes principales :

1. Créer un réseau virtuel Azure de site à site ou de point à site. étapes de Hello dans ce document supposent que vous utilisez un réseau de site à site.
2. Créez un cluster Spark dans Azure HDInsight qui fait partie de hello de site à site réseau virtuel Azure.
3. Vérifiez la connectivité hello entre le nœud principal du cluster hello et votre bureau.
4. Créer une application Scala dans IntelliJ IDEA et la configurer pour le débogage à distance.
5. Exécuter et déboguer l’application hello.

## <a name="prerequisites"></a>Composants requis
* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Kit de développement logiciel (SDK) Oracle Java. Vous pouvez l’installer [ici](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IntelliJ IDEA. Cet article utilise la version 2017.1. Vous pouvez l’installer à partir d’ [ici](https://www.jetbrains.com/idea/download/).
* HDInsight Tools dans le kit de ressources Azure pour IntelliJ. Outils HDInsight pour IntelliJ sont disponibles dans le cadre de la boîte à outils Azure pour IntelliJ de hello. Pour obtenir des instructions sur la façon dont tooinstall hello boîte à outils Azure, consultez [installation Bonjour Azure Toolkit pour IntelliJ](../azure-toolkit-for-intellij-installation.md).
* Connectez-vous à votre abonnement Azure à partir d’IntelliJ IDEA. Suivez les instructions de hello [ici](hdinsight-apache-spark-intellij-tool-plugin.md).
* Lorsque vous exécutez l’application Spark Scala pour le débogage distant sur un ordinateur Windows, vous pouvez obtenir une exception comme expliqué dans [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) qui se produit en raison de tooa manquant WinUtils.exe sur Windows. toowork autour de cette erreur, vous devez [télécharger hello exécutable à partir d’ici](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa emplacement comme **C:\WinUtils\bin**. Vous devez ensuite ajouter une variable d’environnement **HADOOP_HOME** et la valeur hello de variable de hello trop**C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>Étape 1 : créer un réseau virtuel Azure
Suivez les instructions de hello hello ci-dessous des liens toocreate un réseau virtuel Azure, puis vérifiez la connectivité hello entre bureau de hello et réseau virtuel Azure.

* [Créer un réseau virtuel avec une connexion VPN de site à site à l’aide du portail Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [Configurer un réseau virtuel de tooa de connexion de point à site à l’aide de PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>Étape 2 : créer un cluster Spark HDInsight
Vous devez également créer un cluster d’Apache Spark sur Azure HDInsight qui fait partie de hello réseau virtuel Azure que vous avez créé. Utilisez les informations hello disponibles à l’adresse [basés sur Linux de créer des clusters dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Dans le cadre de la configuration facultative, sélectionnez hello réseau virtuel Azure que vous avez créé à l’étape précédente de hello.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>Étape 3 : Vérifier la connectivité de hello entre le nœud principal du cluster hello et votre bureau
1. Obtenir l’adresse IP de hello de nœud principal de hello. Ouvrez Ambari UI de cluster de hello. Dans le panneau de cluster hello, cliquez sur **tableau de bord**.

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. À partir de hello Ambari UI, hello en haut à droite, cliquez sur **hôtes**.

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. Vous devez obtenir une liste de nœuds principaux, de nœuds worker et de nœuds zookeeper. Hello headnodes ont hello **hn*** préfixe. Cliquez sur le nœud principal de la première de hello.

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. En bas de hello de page hello qui s’ouvre, à partir de hello **Résumé** zone, copie hello adresse IP de nœud principal de hello et nom d’hôte hello.

    ![Rechercher l’adresse IP du nœud principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Inclure l’adresse hello et nom d’hôte hello de hello nœud principal toohello **hôtes** fichier sur l’ordinateur où vous voulez toorun, puis déboguez à distance les travaux de Spark hello hello. Cela vous permettra toocommunicate avec un nœud principal de hello à l’aide d’adresse IP de hello, ainsi que des nom d’hôte hello.

   1. Ouvrez un bloc-notes avec des autorisations élevées. Dans le menu fichier de hello, cliquez sur **ouvrir** puis accédez emplacement toohello du fichier d’hôtes hello. Sur un ordinateur Windows, ce fichier se trouve dans le répertoire `C:\Windows\System32\Drivers\etc\hosts`.
   2. Ajouter hello suivant toohello **hôtes** fichier.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. À partir de l’ordinateur hello que vous avez connecté toohello réseau virtuel Azure qui est utilisé par le cluster HDInsight de hello, vérifiez que vous pouvez tester les deux headnodes hello à l’aide d’adresse IP de hello, ainsi que des nom d’hôte hello.
7. SSH dans à l’aide d’instructions hello au nœud principal de cluster hello [cluster de HDInsight tooan de se connecter à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md). À partir du nœud principal de cluster hello, ping l’adresse IP de hello d’ordinateur de bureau hello. Vous devez tester la connectivité tooboth hello attribués d’adresses IP toohello ordinateur, une pour la connexion de réseau hello et hello autre pour hello réseau virtuel Azure hello ordinateur est connecté à.
8. Répétez les étapes de hello pour hello autre nœud principal également.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>Étape 4 : Créer une application Spark Scala à l’aide des outils de HDInsight hello dans la boîte à outils Azure pour IntelliJ et configurez-le pour le débogage distant
1. Lancez IntelliJ IDEA et créez un nouveau projet. Dans la boîte de dialogue Nouveau projet hello, rendre hello des options suivantes, puis cliquez sur **suivant**.

    ![Créer une application Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * Dans le volet gauche de hello, sélectionnez **HDInsight**.
   * Dans le volet droit de hello, sélectionnez **Spark sur HDInsight (Scala)**.
   * Cliquez sur **Suivant**.
2. Dans la fenêtre suivante de hello, fournir hello suivant des détails du projet, puis cliquez sur **Terminer**.  
   - Fournissez un nom de projet et un emplacement de projet.
   - Pour **Projet SDK**, utilisez Java 1.8 pour le cluster Spark 2.x, Java 1.7 pour le cluster Spark 1.x.
   - Pour la **version Spark**, l’assistant de création de projets Scala intègre la version correcte pour le kit de développement logiciel Spark et le kit de développement logiciel Scala. Si la version du cluster spark hello est 2.0 inférieur, choisissez nouvelles 1.x. Dans le cas contraire, vous devez sélectionner spark2.x. Cet exemple utilise Spark2.0.2 (Scala 2.11.8).
       ![Créer une application Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. projet de Spark Hello créera automatiquement un artefact pour vous. artefact de hello toosee, procédez comme suit.

   1. À partir de hello **fichier** menu, cliquez sur **Structure de projet**.
   2. Bonjour **Structure de projet** boîte de dialogue, cliquez sur **artefacts** toosee hello par défaut artefact qui est créé.
   ![Créer un fichier JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      Vous pouvez également créer vos propres artefact Fix en cliquant sur hello  **+**  icône, mis en surbrillance dans l’image hello ci-dessus.

4. Ajoutez les bibliothèques tooyour projet. tooadd une bibliothèque, cliquez sur le nom de projet hello dans l’arborescence du projet hello, puis cliquez sur **ouvrir les paramètres du Module**. Bonjour **Structure de projet** boîte de dialogue, dans le volet gauche de hello, cliquez sur **bibliothèques**, cliquez sur le symbole de hello (+), puis cliquez sur **à partir de Maven**.

    ![Ajouter une bibliothèque](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    Bonjour **télécharger la bibliothèque à partir de Maven référentiel** boîte de dialogue zone, rechercher et ajouter hello suivant des bibliothèques.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Copie `yarn-site.xml` et `core-site.xml` de hello nœud principal de cluster et l’ajouter toohello projet. Utilisez hello commandes toocopy hello fichiers suivants. Vous pouvez utiliser [Cygwin](https://cygwin.com/install.html) suivant de hello toorun `scp` fichiers hello toocopy hello cluster headnodes de commandes.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Étant donné que nous avons ajouté déjà hello cluster nœud principal IP adresse et les noms d’hôtes fo hello fichier hosts sur le bureau de hello, nous pouvons utiliser hello **scp** commandes Bonjour suivant manière.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Ajouter le projet tooyour de ces fichiers en les copiant sous hello **/src** dossier dans l’arborescence de votre projet, par exemple `<your project directory>\src`.
6. Hello de mise à jour `core-site.xml` hello toomake modifications suivantes.

   1. `core-site.xml`inclut le compte de stockage de clés toohello hello chiffré associé hello cluster. Bonjour `core-site.xml` que vous avez ajouté le projet toohello, remplacer hello de clé chiffrée avec la clé de stockage réel hello associée au compte de stockage par défaut hello. Voir [Gérer vos clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Supprimer hello suivant entrées hello `core-site.xml`.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Enregistrez le fichier de hello.
7. Ajoutez la classe de principal de hello pour votre application. À partir de hello **Explorateur de projets**, avec le bouton droit **src**, pointez trop**nouveau**, puis cliquez sur **Scala classe**.

    ![Ajouter le code source](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. Bonjour **créer une nouvelle classe Scala** boîte de dialogue zone, fournissez un nom pour **type** sélectionnez **objet**, puis cliquez sur **OK**.

    ![Ajouter le code source](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. Bonjour `MyClusterAppMain.scala` file, collez hello suivant de code. Ce code crée le contexte de Spark hello et lance un `executeJob` méthode hello `SparkSample` objet.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. Répétez les étapes 8 et 9 ci-dessus tooadd un nouvel objet Scala appelé `SparkSample`. toothis classe ajouter hello suivant de code. Ce code lit les données de salutation hello HVAC.csv (disponible sur tous les clusters HDInsight Spark), récupère les lignes hello qui ont uniquement un chiffre dans la colonne septième hello hello CSV et écrit la sortie de hello trop**/HVACOut** sous la valeur par défaut de hello conteneur de stockage pour le cluster de hello.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. Répétez les étapes 8 et 9 ci-dessus tooadd une nouvelle classe appelée `RemoteClusterDebugging`. Cette classe implémente l’infrastructure de test de Spark hello est utilisé pour déboguer des applications. Ajouter hello suivant code toohello `RemoteClusterDebugging` classe.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     Deux toonote choses ici :

   * Pour `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, assurez-vous que hello l’assembly Spark JAR est disponible sur le stockage de cluster hello au chemin d’accès spécifié de hello.
   * Pour `setJars`, spécifier l’emplacement de hello où jar d’artefact hello sera créé. En général, il s’agit du répertoire `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. Bonjour `RemoteClusterDebugging` de classe, avec le bouton droit hello `test` (mot clé) et sélectionnez **créer une Configuration de RemoteClusterDebugging**.

    ![Créer une configuration distante](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. Dans la boîte de dialogue hello, fournissez un nom pour la configuration de hello et sélectionnez hello **Test type** en tant que **nom du Test**. Laissez toutes les autres valeurs par défaut, cliquez sur **Appliquer**, puis cliquez sur **OK**.

    ![Créer une configuration distante](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. Vous devez maintenant voir un **exécuter à distance** configuration liste déroulante dans la barre de menus hello.

    ![Créer une configuration distante](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>Étape 5 : Exécuter l’application hello en mode débogage
1. Dans votre projet IntelliJ idée, ouvrez `SparkSample.scala` et créer un rdd1 too'val suivant de point d’arrêt ». Dans le menu contextuel de hello pour la création d’un point d’arrêt, sélectionnez **ligne dans la fonction executeJob**.

    ![Ajouter un point d’arrêt](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Cliquez sur hello **déboguer exécuter** toohello suivant du bouton **exécuter à distance** toostart de liste déroulante de configuration application hello en cours d’exécution.

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Lorsque l’exécution du programme hello atteint un point d’arrêt hello, vous devez voir un **débogueur** onglet dans le volet du bas hello.

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Cliquez sur hello (**+**) icône tooadd un espion, comme indiqué dans l’image hello ci-dessous.

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Ici, car l’application hello s’est arrêtée avant la variable de hello `rdd1` a été créé, à l’aide de cette espion que nous pouvons voir ce que sont hello 5 premières lignes dans la variable de hello `rdd`. Appuyez sur **ENTRÉE**.

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    Ce que vous voyez dans l’image hello ci-dessus est que vous pouvez interroger terrabytes de données et de débogage lors de l’exécution, la progression de votre application. Par exemple, dans la sortie hello illustrée hello ci-dessus, vous pouvez voir que hello première ligne de sortie de hello est un en-tête. En fonction de cela, vous pouvez modifier la ligne d’en-tête hello tooskip application code si nécessaire.
5. Vous pouvez maintenant cliquer sur hello **Resume programme** tooproceed icône avec votre application.

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Si l’application hello se termine correctement, vous devez voir une sortie semblable à hello suivante.

    ![Exécuter le programme de hello en mode débogage](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Démonstration
* Créez un projet Scala (vidéo) : [Créer des applications Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Débogage distant (vidéo) : [utilisation Azure Toolkit pour les applications de Spark IntelliJ toodebug à distance sur un HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

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
* [Utilisez les outils HDInsight dans la boîte à outils Azure pour IntelliJ toocreate et soumettre des applications les plus importantes Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilisez la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications de Spark toocreate Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)
