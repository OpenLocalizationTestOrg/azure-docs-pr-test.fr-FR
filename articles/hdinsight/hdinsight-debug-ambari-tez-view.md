---
title: aaaUse Ambari Tez vue HDInsight - Azure | Documents Microsoft
description: "Découvrez comment toouse hello Ambari Tez afficher les travaux de Tez toodebug sur HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>Utilisez les vues Ambari toodebug Tez travaux sur HDInsight

Hello l’interface utilisateur Web de Ambari pour HDInsight contient une vue de Tez qui peut être utilisés des travaux de toounderstand et de débogage qui utilisent Tez. vue de Tez Hello vous permet de travail de hello toovisualize comme un graphique des éléments connectés, explorez chaque élément et extraire des statistiques et informations de journalisation.

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Composants requis

* Un cluster HDInsight sous Linux Pour plus d’informations sur la création d’un cluster, consultez l’article [Prise en main de HDInsight sous Linux](hdinsight-hadoop-linux-tutorial-get-started.md).
* Un navigateur web moderne qui prend en charge HTML5.

## <a name="understanding-tez"></a>Présentation de Tez

Tez est une infrastructure extensible pour le traitement des données dans Hadoop plus rapide que le traitement MapReduce traditionnel. Pour les clusters HDInsight de basés sur Linux, il est moteur par défaut de hello pour la ruche.

Tez crée un dirigées acycliques graphique (DAG) qui décrit l’ordre de hello des actions requises par les travaux. Différentes actions sont appelées des sommets et exécuter une partie de hello travail global. l’exécution réelle de Hello de travail hello décrite par un sommet est appelée une tâche et peut être répartie sur plusieurs nœuds de cluster de hello.

### <a name="understanding-hello-tez-view"></a>Hello de présentation Tez vue

Hello Tez vue fournit des informations d’historique et des informations sur les processus qui sont en cours d’exécution. Ces informations vous indiquent comment une tâche est répartie entre les clusters. Elle affiche également des compteurs utilisés par les tâches et les sommets, et des informations d’erreur liés toohello travail. Il offre des informations utiles dans hello les scénarios suivants :

* Surveillance des processus longs, affichage hello la progression de la carte et réduire les tâches.
* Analyse des données historiques pour les processus réussies ou échouées toolearn comment le traitement peut être amélioré ou en raison de l’échec.

## <a name="generate-a-dag"></a>Générer un DAG

Hello Tez vue contient uniquement les données si une tâche qui utilise hello Tez moteur est en cours d’exécution ou a été exécuté précédemment. Les requêtes Hive simples peuvent être résolues sans utiliser Tez. Les requêtes plus complexes qui effectuent des opérations de filtrage, de regroupement, de tri, de jointure, etc. Utilisez hello Tez moteur.

Utilisez hello suivant les étapes toorun une requête Hive qui utilise Tez :

1. Dans un navigateur web, accédez à toohttps://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** hello désigne votre cluster HDInsight.

2. Dans le menu de hello en hello haut hello, sélectionnez hello **vues** icône. Cette icône représente une série de carrés. Dans la liste déroulante hello qui s’affiche, sélectionnez **Hive vue**.

    ![Sélectionner la vue Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. Lorsque hello ruche vue charge, coller hello ci-dessous dans l’éditeur de requête de hello de requête, puis cliquez sur **exécuter**.

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    Une fois le travail de hello est terminé, vous devez voir sortie hello affiché dans hello **résultats du processus de requête** section. les résultats de Hello doivent être similaires toohello suivant du texte :

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. Sélectionnez hello **journal** onglet. Vous consultez toohello similaire à informations suivant le texte :

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    Enregistrer hello **id d’application** valeur, comme cette valeur est utilisée dans la section suivante de hello.

## <a name="use-hello-tez-view"></a>Utilisez hello Tez vue

1. Dans le menu de hello en hello haut hello, sélectionnez hello **vues** icône. Dans la liste déroulante hello qui s’affiche, sélectionnez **Tez vue**.

    ![Sélectionner la vue Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. Lors du chargement de hello Tez vue, vous voyez une liste de requêtes hive qui sont en cours d’exécution, ou qui ont été exécutés sur le cluster de hello.

    ![Tous les DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. Si vous avez une seule entrée, il est de requête hello que vous avez exécuté dans la section précédente de hello. Si vous avez plusieurs entrées, vous pouvez le rechercher à l’aide des champs de hello en hello haut hello.

4. Sélectionnez hello **ID de requête** pour une requête Hive. Informations sur la requête de hello s’affiche.

    ![Détails du DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. onglets Hello sur cette page permettent de hello tooview informations suivantes :

    * **Détails de la requête**: plus d’informations sur la requête de Hive hello.
    * **Chronologie** : plus d’informations sur la durée de chaque étape du traitement.
    * **Configurations**: configuration hello utilisée pour cette requête.

    À partir de __détails de la requête__ vous pouvez utiliser hello liens toofind informations hello __Application__ ou hello __DAG__ pour cette requête.
    
    * Hello __Application__ lien affiche des informations sur hello application fils pour cette requête. À ce stade, vous pouvez accéder à journaux d’application hello fils.
    * Hello __DAG__ lien affiche des informations sur le graphique acyclique dirigé de hello pour cette requête. À ce stade, vous pouvez afficher une représentation graphique de hello DAG. Vous trouverez également des informations sur les sommets hello dans hello DAG.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment toouse hello Tez afficher, en savoir plus sur [à l’aide de la ruche sur HDInsight](hdinsight-use-hive.md).

Pour plus d’informations techniques sur Tez, consultez hello [page Tez sur Hortonworks](http://hortonworks.com/hadoop/tez/).

Pour plus d’informations sur l’utilisation de Ambari avec HDInsight, consultez [gérer les clusters HDInsight à l’aide de hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)
