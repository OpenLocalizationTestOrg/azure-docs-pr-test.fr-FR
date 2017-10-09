---
title: outils aaaData Lake pour Visual Studio avec Hortonworks Sandbox - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse hello des outils d’Azure Data Lake pour Visual Studio avec un sandbox de Hortonworks hello en cours d’exécution dans une machine virtuelle locale. Grâce à ces outils, vous pouvez créer et exécuter des tâches Hive et Pig sur sandbox de hello et de sortie de travail vue et de l’historique."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Utiliser les outils d’Azure Data Lake hello pour Visual Studio avec hello Hortonworks Sandbox

Azure Data Lake inclut des outils permettant de travailler avec des clusters Hadoop génériques. Ce document fournit la procédure de hello nécessitent toouse hello Data Lake outils hello Hortonworks Sandbox en cours d’exécution sur un ordinateur virtuel local.

À l’aide de hello bac à sable Hortonworks vous permet de toowork avec Hadoop localement sur votre environnement de développement. Une fois que vous avez développé une solution et que vous souhaitez toodeploy il à grande échelle, vous pouvez ensuite déplacer le cluster HDInsight de tooan.

## <a name="prerequisites"></a>Composants requis

* Hello Hortonworks Sandbox, en cours d’exécution sur un ordinateur virtuel sur votre environnement de développement. Ce document a été écrit et testé avec sandbox hello en cours d’exécution dans Oracle VirtualBox. Pour plus d’informations sur la configuration de bac à sable hello, consultez hello [prise en main sandbox de Hortonworks hello.](hdinsight-hadoop-emulator-get-started.md) document.

* Visual Studio 2013, Visual Studio 2015 ou Visual Studio 2017 (toute édition).

* Hello [Azure SDK pour .NET](https://azure.microsoft.com/downloads/) 2.7.1 ou version ultérieure.

* Hello [lac de données Azure tools pour Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="configure-passwords-for-hello-sandbox"></a>Configurer des mots de passe pour le bac à sable hello

Vérifiez que hello que hortonworks Sandbox est en cours d’exécution. Puis suivez les étapes de hello Bonjour [prise en main de hello bac à sable Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document. Ces étapes configurent le mot de passe hello hello SSH `root` de compte et hello Ambari `admin` compte. Ces mots de passe sont utilisés lorsque vous vous connectez le bac à sable toohello à partir de Visual Studio.

## <a name="connect-hello-tools-toohello-sandbox"></a>Connecter le bac à sable toohello hello outils

1. Ouvrez Visual Studio, sélectionnez **Afficher**, puis **Explorateur de serveurs**.

2. À partir de **l’Explorateur de serveurs**, avec le bouton hello **HDInsight** entrée, puis sélectionnez **connecter tooHDInsight émulateur**.

    ![Capture d’écran de l’Explorateur de serveurs avec connexion tooHDInsight émulateur mis en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. À partir de hello **connecter tooHDInsight émulateur** boîte de dialogue, entrez le mot de passe hello que vous avez configuré pour Ambari.

    ![Capture d’écran de la boîte de dialogue avec la zone de texte pour la saisie du mot de passe en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    Sélectionnez **suivant** toocontinue.

4. Hello d’utilisation **mot de passe** champ tooenter hello mot de passe vous avez configuré pour hello `root` compte. Laissez hello autres champs à la valeur par défaut de hello.

    ![Capture d’écran de la boîte de dialogue avec la zone de texte pour la saisie du mot de passe en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    Sélectionnez **suivant** toocontinue.

5. Attendez que la validation de hello services toofinish. Dans certains cas, la validation peut-être échouer et vous demande de configuration de hello tooupdate. Si la validation échoue, sélectionnez **mise à jour**et attendez que la configuration de hello et de vérification pour hello service toofinish.

    ![Capture d’écran de la boîte de dialogue avec le bouton Mettre à jour en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > processus de mise à jour Hello utilise hello toomodify de Ambari toowhat de configuration de bac à sable Hortonworks attendu par les outils de Data Lake hello pour Visual Studio.

6. Une fois la validation terminée, sélectionnez **Terminer** toocomplete configuration.
    ![Capture d’écran de la boîte de dialogue avec le bouton Terminer en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > Selon la vitesse de hello de votre environnement de développement et hello quantité de mémoire allouée toohello virtual machine, il peut prendre plusieurs minutes tooconfigure et valider des services de hello.

Après avoir suivi ces étapes, vous avez maintenant un **cluster local HDInsight** entrée dans l’Explorateur de serveurs sous hello **HDInsight** section.

## <a name="write-a-hive-query"></a>Écriture d’une requête Hive

Hive fournit un langage de requête de type SQL (HiveQL) pour le traitement des données structurées. Utilisez hello suivant toolearn étapes fonctionnement des requêtes sur le cluster local de hello toorun à la demande.

1. Dans **l’Explorateur de serveurs**, cliquez sur entrée hello pour le cluster local hello que vous avez ajouté précédemment, puis sélectionnez **écrire une requête Hive**.

    ![Capture d’écran de l’Explorateur de serveurs avec Écrire une requête Hive en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    Une nouvelle fenêtre de requête s’affiche. Ici, vous pouvez rapidement écrire et envoyer un cluster local toohello de requête.

2. Dans la nouvelle fenêtre de requête hello, entrez hello de commande suivante :

        select count(*) from sample_08;

    requête de hello toorun, sélectionnez **Submit** haut hello de fenêtre hello. Laissez des autres valeurs hello (**lot** et le nom du serveur) à des valeurs par défaut hello.

    ![Capture d’écran de la fenêtre de requête, avec le bouton d’envoi hello mis en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    Vous pouvez également utiliser déroulante hello ensuite trop**Submit** tooselect **avancé**. Les options avancées permettent tooprovide des options supplémentaires lors de l’envoi de la tâche de hello.

    ![Capture d’écran de la boîte de dialogue Envoyer le script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. Une fois que vous envoyez la requête de hello, état de la tâche hello s’affiche. état de la tâche Hello affiche des informations sur les travaux hello s’il est traité par Hadoop. **État de la tâche** indique l’état du travail de hello hello. état de Hello est régulièrement mis à jour, ou vous pouvez utiliser hello actualiser icône toorefresh hello l’état manuellement.

    ![Capture d’écran de la boîte de dialogue Vue du travail, avec État du travail en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    Après avoir hello **état du travail** change également**terminé**, un graphique acyclique dirigé (DAG, Switched Virtual Circuit) s’affiche. Ce diagramme décrit le chemin d’exécution hello qui a été déterminé par Tez lors du traitement de requête de Hive hello. Tez est le moteur d’exécution par défaut de hello pour la ruche du cluster local de hello.

    > [!NOTE]
    > Tez est également hello par défaut lorsque vous utilisez des clusters HDInsight de basés sur Linux. Il n’est pas défaut hello sur HDInsight de basés sur Windows. toouse il, vous devez ajouter la ligne de hello `set hive.execution.engine = tez;` début toohello de votre requête Hive.

    Hello d’utilisation **sortie des tâches** lien de sortie de hello tooview. Dans ce cas, il est 823, nombre de hello de lignes dans la table de sample_08 hello. Vous pouvez afficher des informations de diagnostic sur la tâche de hello en utilisant hello **journal des travaux** et **télécharger un journal fils** des liens.

4. Vous pouvez également exécuter des travaux de la ruche interactive en modifiant hello **lot** champ trop**Interactive**. Sélectionnez ensuite **Exécuter**.

    ![Capture d’écran avec les boutons Interactif et Exécuter en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    Une requête interactive flux hello le journal de sortie généré pendant le traitement toohello **HiveServer2 sortie** fenêtre.

    > [!NOTE]
    > Hello informations est hello même qui est disponible à partir de hello **journal des travaux** lier une fois une tâche terminée.

    ![Capture d’écran du journal de sortie](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Création d’un projet Hive

Vous pouvez également créer un projet qui contient plusieurs scripts Hive. Utiliser un projet lorsque vous avez des scripts associés ou les scripts toostore dans un système de contrôle de version.

1. Dans Visual Studio, sélectionnez **Fichier**, **Nouveau**, puis **Projet**.

2. À partir de la liste de hello de projets, développez **modèles**, développez **Azure Data Lake**, puis sélectionnez **HIVE (HDInsight)**. Dans la liste hello des modèles, sélectionnez **exemple de la ruche**. Entrez un nom et un emplacement, puis sélectionnez **OK**.

    ![Capture d’écran de la fenêtre Nouveau projet avec Azure Data Lake, HIVE, Hive Sample (Exemple Hive) et OK en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

Hello **exemple de la ruche** projet contient deux scripts, **WebLogAnalysis.hql** et **SensorDataAnalysis.hql**. Vous pouvez soumettre ces scripts à l’aide de hello même **Submit** bouton en haut de hello de fenêtre hello.

## <a name="create-a-pig-project"></a>Création d’un projet Pig

Contrairement à Hive qui offre un langage de type SQL pour travailler avec des données structurées, Pig effectue des transformations sur les données. Pig fournit un langage (Pig Latin) qui vous permet de toodevelop un pipeline de transformations. toouse Pig avec le cluster local de hello, procédez comme suit :

1. Ouvrez Visual Studio et sélectionnez **Fichier**, **Nouveau**, puis **Projet**. À partir de la liste de hello de projets, développez **modèles**, développez **Azure Data Lake**, puis sélectionnez **Pig (HDInsight)**. Dans la liste hello des modèles, sélectionnez **Pig Application**. Entrez un nom et un emplacement, puis sélectionnez **OK**.

    ![Capture d’écran de la fenêtre Nouveau projet avec Azure Data Lake, Pig, Pig Application (Application Pig) et OK en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. Entrez hello après le texte en tant que contenu hello Hello **script.pig** fichier qui a été créé avec ce projet.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    Alors que Pig utilise une autre langue que la ruche, mode d’exécution de travaux de hello est cohérent entre les deux langages, de par Bonjour **Submit** bouton. Liste déroulante en regard de hello en sélectionnant **Submit** affiche une boîte de dialogue avancées d’envoi pour Pig.

    ![Capture d’écran de la boîte de dialogue Envoyer le script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. état de la tâche hello et de sortie s’affiche également, même hello en tant qu’une requête Hive.

    ![Capture d’écran d’un travail Pig terminé](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>Affichage des tâches

Outils de LAC de données vous permettent également tooeasily afficher des informations sur les travaux qui ont été exécutées sur Hadoop. Utilisez hello suivant les étapes toosee hello travaux qui ont été exécutées sur le cluster local de hello.

1. À partir de **l’Explorateur de serveurs**, cliquez sur le cluster local de hello, puis sélectionnez **afficher les travaux**. Une liste des tâches qui ont été soumis toohello cluster s’affiche.

    ![Capture d’écran de l’Explorateur de serveurs avec Afficher les travaux en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. Dans la liste hello des tâches, sélectionnez une tooview détails de la tâche hello.

    ![Capture d’écran de travail de navigateur, avec l’un des travaux hello mis en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    les informations de Hello affichées sont similaires toowhat qu'après l’exécution d’une requête Hive ou Pig, y compris des liens tooview hello sortie et le journal.

3. Vous pouvez également modifier et soumettez à nouveau la tâche hello à partir d’ici.

## <a name="view-hive-databases"></a>Affichage des bases de données Hive

1. Dans **l’Explorateur de serveurs**, développez hello **cluster local HDInsight** entrée, puis développez **bases de données de la ruche**. Hello **par défaut** et **xademo** bases de données sur le cluster local de hello sont affichés. Une base de données en développant les tables au sein de la base de données hello hello.

    ![Capture d’écran de l’Explorateur de serveurs avec des bases de données développées](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. Développer un tableau affiche hello colonnes de la table. tooquickly afficher hello de données, cliquez sur une table et sélectionnez **100 lignes du haut vue**.

    ![Capture d’écran de l’Explorateur de serveurs avec une table développée et l’option Afficher les 100 premières lignes sélectionnée](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>Propriétés de base de données et de table

Vous pouvez afficher les propriétés de hello d’une base de données ou une table. En sélectionnant **propriétés** affiche les détails d’élément de hello sélectionné dans la fenêtre de propriétés hello. Par exemple, consultez les informations de hello illustrées hello suivant capture d’écran :

![Capture d’écran de le fenêtre Propriétés](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>Création d’une table

toocreate une table, cliquez sur une base de données, puis sélectionnez **Create Table**.

![Capture d’écran de l’Explorateur de serveurs avec Créer une table en surbrillance](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

Vous pouvez ensuite créer la table hello à l’aide d’un formulaire. Au bas de hello de hello suivant capture d’écran, vous pouvez voir hello HiveQL brut qui est utilisé toocreate hello table.

![Capture d’écran du formulaire de hello utilisé toocreate une table](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>Étapes suivantes

* [Apprentissage des câbles hello Hello Hortonworks Sandbox](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Didacticiel Hadoop - Prise en main de HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
