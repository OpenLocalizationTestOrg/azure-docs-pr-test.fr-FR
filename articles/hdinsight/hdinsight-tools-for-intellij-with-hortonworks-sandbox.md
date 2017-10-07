---
title: aaaUse Azure Toolkit pour IntelliJ avec Hortonworks Sandbox | Documents Microsoft
description: "En savoir plus toouse HDInsight outils dans la boîte à outils Azure pour IntelliJ avec Hortonworks Sandbox."
keywords: "outils Hadoop, requête hive, intellij, hortonworks sandbox, kit de ressources azure pour intellij"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Utiliser HDInsight Tools pour IntelliJ avec Hortonworks Sandbox

Découvrez comment les outils de HDInsight toouse pour les applications Apache Scala IntelliJ toodevelop et puis effectuer des tests hello applications sur [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) en cours d’exécution sur votre station de travail. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/) est un environnement de développement Java intégré (IDE) pour développer des logiciels. Après avoir développé et testé vos applications sur Hortonworks Sandbox, vous pouvez les déplacer trop[Azure HDInsight](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Composants requis

Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :

- Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox s’exécutant sur votre environnement local. tooconfigure HDP, consultez [prise en main de l’écosystème de Hadoop hello avec un bac à sable Hadoop sur un ordinateur virtuel](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >HDInsight Tools pour IntelliJ a seulement été testé avec HDP 2.4. tooget HDP 2.4, développez **Hortonworks Sandbox Archive** sur hello [Hortonworks Sandbox télécharge site](http://hortonworks.com/downloads/#sandbox).

- [Kit de développeur Java (JDK) version 1.8 ou ultérieure](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). JDK est requis par hello boîte à outils Azure pour IntelliJ.

- [Édition de communauté IntelliJ idée](https://www.jetbrains.com/idea/download) avec hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in et hello [Azure Toolkit pour IntelliJ](../azure-toolkit-for-intellij.md) plug-in. Outils HDInsight pour IntelliJ est disponible dans le cadre de la boîte à outils Azure pour IntelliJ de hello. 

  tooinstall hello plug-ins, hello suivant :

  1. Ouvrez IntelliJ IDEA.
  2. Sur hello **Bienvenue** écran, sélectionnez **configurer**, puis sélectionnez **plug-ins**.
  3. Sélectionnez **plug-in de l’installation de JetBrains** dans l’angle inférieur gauche de hello.
  4. Utilisez toosearch de fonction de recherche hello pour **Scala**, puis sélectionnez **installer**.
  5. Sélectionnez **redémarrer une idée de IntelliJ** installation de hello toocomplete.
  6. Hello de tooinstall Répétez l’étape 4 et 5 **Azure Toolkit pour IntelliJ**. Pour plus d’informations, consultez [installation Bonjour Azure Toolkit pour IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Créer une application Spark Scala

Dans cette section, vous créez un exemple de projet Scala à l’aide d’IntelliJ IDEA. Dans la section suivante de hello, vous liez IntelliJ idée toohello Hortonworks Sandbox (émulateur) avant d’envoyer le projet de hello.

1. Ouvrez IntelliJ IDEA à partir de votre station de travail. Bonjour **nouveau projet** boîte de dialogue zone, hello suivant :

   a. Sélectionnez **HDInsight** > **Spark sur HDInsight (Scala)**.

   b. Bonjour **outil de génération** , sélectionnez une des hello suivant, selon le besoin de tooyour :

    * **Maven**, pour la prise en charge de l’Assistant de création de projets Scala
    * **SBT**, pour la gestion des dépendances de hello et la création de projet de Scala hello

   ![boîte de dialogue Nouveau projet Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Sélectionnez **Suivant**.

3. Bonjour suivant **nouveau projet** boîte de dialogue zone, hello suivant :

    ![Créer les propriétés du projet IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. Bonjour **nom du projet** , entrez un nom de projet.

    b. Bonjour **emplacement du projet** , entrez un emplacement de projet.

    c. Toohello suivant **projet SDK** la liste déroulante, sélectionnez **nouveau**, sélectionnez **JDK**, puis spécifiez le dossier hello de Java JDK version 1.7 ou ultérieure. Sélectionnez **Java 1.8** pour le cluster de hello Spark 2.x, ou sélectionnez **Java 1.7** pour le cluster de hello Spark 1.x. Hello par défaut est C:\Program Files\Java\jdk1.8.x_xxx.

    d. Bonjour **version de Spark** la liste déroulante, Assistant de création de projet Scala intègre version correcte de hello pour le Kit de développement logiciel Spark et Scala SDK. Si la version du cluster Spark hello est antérieure à la version 2.0, sélectionnez **nouvelles 1.x**. Sinon, sélectionnez **Spark 2.x**. La version utilisée dans cet exemple est Spark 1.6.2 (Scala 2.10.5). Assurez-vous que vous utilisez référentiel hello marquée Scala 2.10.x. N’utilisez pas de référentiel hello marquée Scala 2.11.x.

4. Sélectionnez **Terminer**.

5. Si hello **projet** affichage n’est pas déjà ouvert, appuyez sur **Alt + 1** tooopen il.

6. Dans **Explorateur de projets**, développez le projet de hello, puis sélectionnez **src**.

7. Avec le bouton droit **src**, pointez trop**nouveau**, puis sélectionnez **Scala classe**.

8. Bonjour **nom** , entrez un nom, Bonjour **type** boîte, sélectionnez **objet**, puis sélectionnez **OK**.

    ![fenêtre Créer une nouvelle classe Scala de Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. Dans le fichier de .scala hello, collez hello suivant de code :

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. Sur hello **générer** menu, sélectionnez **projet Build**. Assurez-vous que la compilation hello est terminée avec succès.


## <a name="link-toohello-hortonworks-sandbox"></a>Lien toohello Hortonworks Sandbox

Avant de pouvoir lier tooa Hortonworks Sandbox (émulateur), vous devez disposer d’une application IntelliJ existante.

émulateur de tooan toolink, hello suivant :

1. Projet ouvert hello dans IntelliJ.

2. Sur hello **vue** menu, sélectionnez **outils Windows**, puis sélectionnez **Explorateur Azure**.

3. Développez **Azure**, cliquez avec le bouton droit sur **HDInsight**, puis sélectionnez **Lier un émulateur**.

4. Bonjour **lien un nouvel émulateur** fenêtre, entrez un mot de passe hello vos configurés pour le compte de racine hello Hello bac à sable Hortonworks, entrez toothose similaire de valeurs Bonjour suivant capture d’écran, puis **OK** . 

   ![fenêtre de « Lier un nouvel émulateur » Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. émulateur Windows hello tooconfigure, sélectionnez **Oui**.

Lors de l’émulateur de hello est connecté avec succès, l’émulateur hello (Hortonworks Sandbox) est répertorié dans le nœud de HDInsight hello.

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>Soumettre hello Spark Scala application toohello Hortonworks Sandbox

Une fois que vous avez lié l’émulateur de toohello IntelliJ idée, vous pouvez soumettre votre projet.

toosubmit un émulateur tooan du projet, procédez comme hello suivant :

1. Dans **Explorateur de projets**, cliquez sur le projet de hello, puis sélectionnez **soumettre de Spark application tooHDInsight**.

2. Hello suivant :

    a. Bonjour **le cluster Spark (Linux uniquement)** liste déroulante, sélectionnez votre bac à sable Hortonworks local.

    b. Bonjour **nom de la classe principale** zone, sélectionnez ou entrez le nom de la classe principale hello. Pour ce didacticiel, le nom de hello est **GroupByTest**.

3. Sélectionnez **Envoyer**. envoi des journaux de la tâche Hello sont affichés dans la fenêtre d’outil hello Spark soumission.

## <a name="next-steps"></a>Étapes suivantes

- comment les applications de Spark toocreate pour HDInsight à l’aide des outils HDInsight pour IntelliJ, accédez trop de toolearn[utiliser les outils HDInsight dans la boîte à outils Azure pour les applications Spark cluster HDInsight Spark Linux IntelliJ toocreate](hdinsight-apache-spark-intellij-tool-plugin.md).

- toowatch une vidéo d’outils HDInsight pour IntelliJ, accédez trop[présentent les outils HDInsight pour IntelliJ pour le développement de Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).

- toolearn comment les applications de Spark toodebug à l’aide de hello boîte à outils à distance sur HDInsight via SSH, accédez trop[déboguer à distance Spark sur un cluster HDInsight avec la boîte à outils Azure pour IntelliJ via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- toolearn comment les applications de Spark toodebug à l’aide de hello boîte à outils à distance sur HDInsight via VPN, accédez trop[utiliser les outils HDInsight dans la boîte à outils Azure pour les applications de Spark IntelliJ toodebug à distance sur le cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- toolearn comment toouse outils HDInsight pour Eclipse toocreate une application Spark, accédez trop[utiliser les outils HDInsight dans la boîte à outils Azure pour les applications de Spark Eclipse toocreate](hdinsight-apache-spark-eclipse-tool-plugin.md).

- toowatch une vidéo d’outils HDInsight pour Eclipse, accédez trop[HDInsight utiliser un outil pour les applications de Spark Eclipse toocreate](https://mix.office.com/watch/1rau2mopb6fha).
