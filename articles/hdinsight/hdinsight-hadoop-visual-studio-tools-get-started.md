---
title: "aaaConnect tooAzure HDInsight à l’aide de Data Lake Tools pour Visual Studio | Documents Microsoft"
description: "Découvrez comment tooinstall et utilisez Data Lake Tools pour Visual Studio tooconnect tooHadoop clusters dans Azure HDInsight et d’exécution des requêtes Hive."
keywords: "outils Hadoop,requête hive,Visual Studio,Hadoop Visual Studio"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>Se connecter tooAzure HDInsight et exécuter des requêtes Hive à l’aide de Data Lake Tools pour Visual Studio

Découvrez comment des clusters dans toouse Data Lake Tools pour Visual Studio tooconnect tooHadoop [Azure HDInsight](hdinsight-hadoop-introduction.md) et envoyer des requêtes Hive. Pour plus d’informations sur l’utilisation de HDInsight, consultez [Introduction tooHDInsight](hdinsight-hadoop-introduction.md) et [prise en main HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md). Pour plus d’informations sur le cluster de Storm tooa connexion, consultez [développer c# topologies d’Apache Storm sur HDInsight à l’aide de Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Data Lake Tools pour Visual Studio peut être utilisé tooaccess Analytique lac de données et HDInsight.  Pour plus d’informations hello sur Data Lake Tools, consultez [didacticiel : développer des scripts de U-SQL à l’aide de Data Lake Tools pour Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).

**Configuration requise**

toocomplete cette hello Data Lake didacticiel et l’utilisation des outils dans Visual Studio, vous devez suivant de hello :

* Un cluster Azure HDInsight : voir d’un seul, toocreate [prise en main HDInsight de basés sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md)
* Une station de travail avec hello suivant logicielle :
  
  * Windows 10, Windows 8.1, Windows 8 ou Windows 7.
  * Visual Studio 2013/2015/2017.
    
    > [!NOTE]
    > Actuellement, hello Data Lake Tools pour Visual Studio sont fournis uniquement avec la version anglaise de hello.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Installation de Data Lake Tools pour Visual Studio

Data Lake Tools est installé par défaut pour Visual Studio 2017. Pour les versions antérieures, vous pouvez l’installer à l’aide de hello [Web Platform Installer](https://www.microsoft.com/web/downloads/). Vous devez choisir hello qui correspond à votre version de Visual Studio. Si vous n’avez pas installé Visual Studio, vous pouvez installer hello dernières Visual Studio Community et Kit de développement logiciel Azure à l’aide de hello [Web Platform Installer](https://www.microsoft.com/web/downloads/):

![Outils de LAC de données pour Visual Studio Web Platform installer. ] (./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "Utilisez Web Platform Installer tooinstall Data Lake Tools pour Visual Studio")

## <a name="connect-tooazure-subscriptions"></a>Se connecter tooAzure abonnements
Data Lake Tools pour Visual Studio vous permet de clusters HDInsight de tooyour tooconnect, effectuer certaines opérations de gestion de base et exécuter des requêtes Hive.

> [!NOTE]
> Pour plus d’informations sur la connexion du cluster de Hadoop générique tooa, consultez [rédiger et soumettre des requêtes Hive à l’aide de Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).
> 
> 

**tooconnect tooyour abonnement Azure**

1. Ouvrez Visual Studio.
2. À partir de hello **vue** menu, cliquez sur **l’Explorateur de serveurs** tooopen hello Explorateur de serveurs.
3. Développez **Azure**, puis **HDInsight**.
   
   > [!NOTE]
   > Hello d’avis **liste des tâches HDInsight** fenêtre doit être ouverte. Si vous ne le voyez pas, cliquez sur **autres fenêtres** de hello **vue** menu, puis sur **fenêtre liste des tâches HDInsight**.  
   > 
   > 
4. Entrez les informations d’identification de votre abonnement Azure, puis cliquez sur **Se connecter**. Cela est uniquement nécessaire si vous êtes jamais connecté toohello abonnement Azure à partir de Visual Studio sur cette station de travail.
5. Dans l’explorateur de serveurs, vous verrez une liste des clusters HDInsight existants. Si vous n’avez pas tous les clusters, vous pouvez créer un à l’aide de hello portail Azure, Azure PowerShell ou hello HDInsight SDK. Pour plus d’informations, consultez la rubrique [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
   
   ![Liste de clusters de l’explorateur de serveurs de Data Lake Tools pour Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Explorateur de serveurs de Data Lake Tools pour Visual Studio")
6. Développez un cluster HDInsight. Vous devez voir les **bases de données Hive**, un compte de stockage par défaut, les comptes de stockage liés et le **journal Hadoop Service**. Vous pouvez développer davantage les entités hello.

Une fois que vous avez connecté tooyour abonnement Azure, vous serez suivant de hello toodo en mesure de :

**tooconnect toohello portail Azure à partir de Visual Studio**

* Dans l’Explorateur de serveurs, développez **Azure** > **HDInsight**, cliquez avec le bouton droit sur un cluster HDInsight, puis cliquez sur **Gérer le cluster dans le portail Azure**.

**tooask questions et fournir des commentaires à partir de Visual Studio**

* À partir de hello **outils** menu, cliquez sur **HDInsight**, puis cliquez sur **Forum MSDN** tooask questions, ou cliquez sur **commenter**.

## <a name="navigate-hello-linked-resources"></a>Parcourir les ressources hello lié
À partir de l’Explorateur de serveurs, vous pouvez voir le compte de stockage par défaut hello et tous les comptes de stockage. Si vous développez le compte de stockage par défaut hello, vous pouvez voir les conteneurs hello hello compte de stockage. compte de stockage par défaut Hello et conteneur par défaut de hello sont marqués. Vous pouvez également cliquer sur hello conteneurs tooview hello contenu.

![Ressources liées de la liste de clusters de l’explorateur de serveurs de Data Lake Tools pour Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "ressources liées de la liste")

Après l’ouverture d’un conteneur, vous pouvez utiliser hello suivant tooupload de boutons, de suppression et d’objets BLOB de téléchargement :

![Opérations blob de l’explorateur de serveurs de Data Lake Tools pour Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "charger, supprimer et télécharger des objets blob")

## <a name="run-a-hive-query"></a>Exécution d'une tâche Hive
[Apache Hive](http://hive.apache.org) est une infrastructure d’entrepôt de données basée sur Hadoop qui permet de synthétiser, d’interroger et d’analyser des données. Data Lake Tools pour Visual Studio prend en charge l’exécution de requêtes Hive à partir de Visual Studio. Pour plus d’informations sur Hive, consultez l’article [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md).

Il s’agit de script de ruche tootest beaucoup de temps par rapport à un cluster HDInsight. Il peut durer plusieurs minutes. Data Lake Tools pour Visual Studio est capable de valider le script Hive localement sans connexion cluster dynamique de tooa.

Data Lake Tools pour Visual Studio permet également aux utilisateurs toosee Nouveautés hello ruche du travail en collectant et surfaces de journaux des fils hello de certaines tâches Hive.

### <a name="view-hello-hivesampletable"></a>Hello de vue **hivesampletable**
Les clusters HDInsight sont fournis avec un exemple de table Hive qui porte le nom *hivesampletable*. Nous utiliserons cette tooshow table vous hello tables de ruche toolist, affichez les schémas de table hello et répertorier les lignes hello dans la ruche du tableau.

**toolist tables de la ruche et afficher le schéma de la table Hive**

1. À partir de **l’Explorateur de serveurs**, développez **Azure** > **HDInsight** > cluster hello de votre choix > **bases de données de la ruche**  >  **Par défaut** > **hivesampletable** toosee le schéma de table hello.
2. Avec le bouton droit **hivesampletable**, puis cliquez sur **100 lignes du haut vue** lignes de hello toolist. Il est hello toorunning équivalent suivant la requête Hive à l’aide du pilote ODBC de la ruche :
   
     SELECT * FROM hivesampletable LIMIT 100
   
   Vous pouvez personnaliser le nombre de lignes hello.
   
   ![Data Lake Tools : requête de schéma Hive dans HDInsight Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Résultats de la requête Hive")

### <a name="create-hive-tables"></a>Créer des tables Hive
Vous pouvez utiliser l’interface graphique utilisateur de hello toocreate une table Hive ou utiliser des requêtes Hive. Pour plus d’informations relatives à l’utilisation de requêtes Hive, consultez [Exécution de requêtes Hive](#run.queries).

**toocreate une table Hive**

1. Dans **l’Explorateur de serveurs**, développez successivement **Azure** > **Clusters HDInsight** un cluster HDInsight > **Bases de données Hive**, puis cliquez avec le bouton droit sur **Par défaut** et cliquez sur **Créer une table**.
2. Configurer la table de hello.
3. Cliquez sur **Create Table** toosubmit hello toocreate hello nouvelle ruche table des tâches.
   
    ![Data Lake Tools : création d’une table Hive dans HDInsight Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Créer une table Hive")

### <a name="run.queries"></a>Validation et exécution de requêtes Hive
Il existe deux façons toocreate et exécution des requêtes Hive :

* Création de requêtes ad hoc
* Création d’une application Hive

**toocreate, valider et exécuter des requêtes ad hoc**

1. Dans **l’Explorateur de serveurs**, développez **Azure**, puis **Clusters HDInsight**.
2. Cluster de hello avec le bouton sur lequel vous souhaitez toorun hello requête, puis cliquez sur **écrire une requête Hive**.
3. Entrez les requêtes Hive hello. Éditeur de notification hello Hive prend en charge IntelliSense. Data Lake Tools pour Visual Studio prend en charge la chargement hello des métadonnées distantes lorsque vous modifiez votre script Hive. Par exemple, lorsque vous tapez « SELECT * FROM », hello, IntelliSense répertorie tous les hello les noms de table suggérées. Lorsqu’un nom de table est spécifié, les noms de colonne hello sont répertoriées par hello IntelliSense. outils de Hello prennent en charge la quasi-totalité des instructions DML de la ruche, sous-requêtes et hello UDF intégrées.
   
    ![Data Lake Tools : IntelliSense dans HDInsight Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "IntelliSense U-SQL")
   
    ![Data Lake Tools : IntelliSense dans HDInsight Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "IntelliSense U-SQL")
   
   > [!NOTE]
   > Seules les métadonnées de hello de clusters de hello qui sont sélectionnée dans la barre d’outils HDInsight seront suggérée.
   > 
   > 
4. (Facultatif) : cliquez sur **valider le Script** erreurs de syntaxe de script toocheck hello.
   
    ![Data Lake Tools : validation locale de Data Lake Tools pour Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "Valider le script")
5. Cliquez sur **Envoyer** ou sur **Envoyer (Avancé)**. Hello submit option avancée, vous allez configurer **nom de la tâche**, **Arguments**, **des Configurations supplémentaires**, et **état Active**pour le script de hello :
   
    ![Requête HDInsight Hadoop Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Soumettre des requêtes")
   
    Après avoir soumis le travail de hello, vous voyez un **récapitulatif de la ruche** fenêtre.
   
    ![Résumé d’une requête HDInsight Hadoop Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Résumé de la tâche Hive")
6. Hello d’utilisation **Actualiser** bouton État de hello tooupdate jusqu'à ce que les changements d’état de tâche de hello trop**terminé**.
7. Cliquez sur les liens hello à l’adresse suivante de hello hello bas toosee : **requête de travail**, **sortie des tâches**, **journal des travaux**, ou **journal des fils**.

**toocreate et exécuter une solution Hive**

1. À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.
2. Sélectionnez **HDInsight** dans le volet gauche de hello, sélectionnez **Application de la ruche** dans le volet du milieu hello, entrez les propriétés de hello, puis cliquez sur **OK**.
   
    ![Data Lake Tools : nouveau projet Hive dans HDInsight Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Créer des applications Hive à partir de Visual Studio")
3. À partir de **l’Explorateur de solutions**, double-cliquez sur **Script.hql** tooopen il.
4. script de toovalidate hello Hive, vous pouvez cliquer sur hello **valider le Script** bouton, ou avec le bouton droit de script hello dans l’éditeur de ruche hello, puis cliquez sur **valider le Script** à partir du menu contextuel de hello.

### <a name="view-hive-jobs"></a>Afficher les tâches Hive
Vous pouvez afficher les requêtes, la sortie, le journal et le journal Yarn des tâches Hive. Pour plus d’informations, consultez hello capture d’écran précédente.

version la plus récente des outils de hello Hello vous permet de toosee, ce qui est à l’intérieur de vos travaux de la ruche en collectant et surfaces fils journaux. Le journal YARN peut vous aider à examiner les problèmes de performances. Pour plus d’informations sur la collection des journaux YARN par HDInsight, consultez [Accès par programme aux journaux des applications HDInsight](hdinsight-hadoop-access-yarn-app-logs.md).

**travaux de ruche tooview**

1. Dans **l’Explorateur de serveurs**, développez **Azure**, puis **HDInsight**.
2. Cliquez avec le bouton droit sur un cluster HDInsight, puis cliquez sur **Afficher les tâches**. Vous verrez une liste de hello Hive travaux exécutés sur un cluster de hello.
3. Cliquez sur une tâche dans hello travail liste tooselect dessus, puis utilisez hello **récapitulatif de la ruche** fenêtre tooopen **requête de travail**, **sortie des tâches**, **journal des travaux**, ou **journal des fils**.
   
    ![Data Lake Tools : affichage des tâches Hive dans HDInsight Visual Studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "Afficher les tâches Hive")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>Plus grande rapidité d’exécution de Hive via HiveServer2
> [!NOTE]
> Cette fonctionnalité n’est disponible qu’avec le cluster HDInsight versions 3.2 et ultérieures.
> 
> 

Hello Data Lake Tools utilisé toosubmit des travaux de ruche via [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (également appelé Templeton). Il a pris un tooreturn beaucoup de temps détails du travail et des informations d’erreur.
Dans l’ordre toosolve ce problème de performances, hello Data Lake Tools exécute Hive travaux directement dans le cluster de hello via HiveServer2, afin qu’il ignore RDP/SSH.
Performances toobetter de plus, les utilisateurs peuvent également afficher Hive sur Tez graphiques et hello les détails de la tâche.

Pour le cluster HDInsight version 3.2 ou ultérieure, vous pouvez voir un bouton **Exécuter par le biais de HiveServer2** :

![Exécution de Data Lake Tools pour Visual Studio via hiveserver2](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "Exécuter des requêtes Hive à l’aide de HiveServer2")

Et vous pouvez voir les journaux hello transmis en continu en temps réel et voir des graphiques de travail hello si la requête Hive de hello est exécutée dans Tez.

![Exécution du chemin d’accès rapide de Data Lake Tools pour Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "Afficher les graphiques de tâches")

**Différence entre l’exécution de requêtes via HiveServer2 et l’envoi de requêtes via WebHCat**

Même si l’exécution de requêtes via HiveServer2 présente de nombreux avantages en termes de performances, elle s’accompagne également de certaines restrictions. Certaines des limitations de hello ne conviennent pas pour une utilisation en production. Hello tableau suivant indique les différences hello :

|  | Exécution via HiveServer2 | Envoi via WebHCat |
| --- | --- | --- |
| Exécuter des requêtes |Élimine les surcharges de hello dans WebHCat (qui lance une MapReduce Job nommé « TempletonControllerJob »). |Tant qu’une requête est exécutée via WebHCat, WebHCat lancera une tâche MapReduce qui introduira une latence supplémentaire. |
| Diffuser des journaux en continu |En temps quasi-réel. |les journaux d’exécution de travail Hello sont disponibles uniquement lorsque le travail hello est terminé. |
| Afficher l’historique des tâches |Si une requête est exécutée par le biais de HiveServer2, son historique des tâches (journal des tâches, résultat de la tâche) n’est pas conservé. application Hello peut être affichée dans l’interface utilisateur des fils avec des informations limitées. |Si une requête est exécutée via WebHCat, son historique des tâches (journal des tâches, résultat de la tâche) est conservé et peut être affiché à l’aide de Visual Studio, du Kit de développement logiciel HDInsight ou de PowerShell. |
| Fermer la fenêtre |S’exécute via HiveServer2 est un moyen de « synchrone » vous devez garder hello ouvertes ; Si les fenêtres hello sont fermées l’exécution des requêtes hello est annulée. |Envoi via WebHCat consiste « asynchrone » afin de pouvoir soumettre la requête hello via WebHCat et fermez Visual Studio. Vous pouvez y revenir et consultez les résultats de hello à tout moment. |

### <a name="tez-hive-job-performance-graph"></a>Graphique de performances des travaux Hive sur Tez
prise en charge de Data Lake Tools Hello montrant les graphiques de performances pour hello ruche travaux s’est exécutée par le moteur d’exécution Tez hello. Pour plus d’informations sur l’activation de Tez, voir [Utilisation de Hive dans HDInsight](hdinsight-use-hive.md). Une fois que vous envoyez une ruche de travail dans Visual Studio, Visual Studio affiche hello graphique lorsque hello tâche est terminée.  Vous devrez peut-être tooclick hello **Actualiser** bouton État du travail tooget hello plus récente.

> [!NOTE]
> Cette fonctionnalité est disponible uniquement pour le cluster HDInsight à partir de la version 3.2.4.593 et ne peut fonctionner que pour les tâches terminées (si vous avez envoyé votre tâche via WebHCat ; ce graphique s’affichera lorsque vous exécuterez votre requête via HiveServer2). Elle fonctionne pour les clusters basés sur Windows et Linux.
> 
> 

![Graphique de performances Hadoop Hive Tez](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "Statut de tâche")

toohelp vous comprenez votre ruche requête mieux, les outils hello ajoutent la vue de la ruche un opérateur de hello dans cette version. Vous devez simplement toodouble, cliquez sur les sommets hello hello du graphique des travaux, et vous pouvez voir tous les opérateurs hello à l’intérieur de hello sommet. Vous pouvez également pointer sur un opérateur spécifique de tooview plus de détails de cet opérateur.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Vue Exécution de la tâche pour Hive sur les tâches Tez
Hello d’affichage de la tâche d’exécution pour ruche sur Tez travaux peut être utilisé tooget structuré et visualiser des informations sur les travaux de la ruche et obtenir plus de détails de tâche. Lorsqu’il existe des problèmes de performances, vous pouvez utiliser hello vue tooget plus de détails. Par exemple, comment chaque tâche s’exécute et hello des informations détaillées sur chaque tâche (en lecture/écriture de données, heure de planification/début/fin, etc.), afin que vous pouvez paramétrer des configurations de projet ou l’architecture du système en fonction des informations de hello visualisé.

![Vue de l’exécution de la tâche Data Lake Tools pour Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "Vue de l’exécution de la tâche")

## <a name="run-pig-scripts"></a>Exécuter des scripts Pig
Data Lake Tools pour Visual Studio prend en charge la création et soumettre des clusters de tooHDInsight scripts Pig. Les utilisateurs peuvent créer un projet Pig à partir du modèle et ensuite soumettre des clusters de tooHDInsight script hello.

## <a name="feedbacks--known-issues"></a>Commentaires et problèmes connus
* Actuellement, les résultats HiveServer2 sont affichés en mode texte pur, ce qui n'est pas idéal. Nous y travaillons actuellement.
* Si les résultats de hello sont démarrées avec des valeurs NULL, actuellement, les résultats hello ne sont pas affichés. Nous ont résolu ce problème et si vous êtes bloqué sur ce problème, vous pouvez toodrop libre équipe nous un e-mail ou un contact de support technique.
* script HQL Hello créé par Visual Studio est encodé en fonction du paramètre de région de l’utilisateur. Il ne peut pas exécuter correctement si l’utilisateur télécharge toocluster de script hello sous forme binaire.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment tooconnect tooHDInsight clusters à partir de Visual Studio, à l’aide de hello Data Lake (HDInsight) package d’outils et comment toorun une requête Hive. Pour plus d'informations, consultez les pages suivantes :

* [Utilisation de Hadoop Hive dans HDInsight](hdinsight-use-hive.md)
* [Prise en main de Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Envoi de tâches Hadoop dans HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Analyse des données Twitter avec Hadoop dans HDInsight](hdinsight-analyze-twitter-data.md)

