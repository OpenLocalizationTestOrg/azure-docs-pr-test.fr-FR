---
title: "aaaUse UI Tez hdinsight basés sur Windows - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello Tez UI toodebug Tez travaux sur HDInsight de HDInsight basés sur Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>Utilisez hello Tez UI toodebug Tez travaux sur HDInsight de basés sur Windows
Hello Tez UI est une page web qui peuvent être utilisés des travaux de toounderstand et de débogage qui utilisent Tez en tant que moteur d’exécution hello sur les clusters HDInsight de basés sur Windows. Hello Tez UI vous permet de travail de hello toovisualize comme un graphique des éléments connectés, explorez chaque élément et extraire des statistiques et informations de journalisation.

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Windows. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Composants requis
* Un cluster HDInsight Windows Pour plus d’informations sur la création d’un cluster, consultez [Prise en main de HDInsight sur Windows](hdinsight-hadoop-tutorial-get-started-windows.md).

  > [!IMPORTANT]
  > Hello Tez UI est disponible uniquement sur les clusters HDInsight de basés sur Windows créés après le 8 février 2016.
  >
  >
* Un client Bureau à distance basé sur Windows.

## <a name="understanding-tez"></a>Présentation de Tez
Tez est une infrastructure extensible pour le traitement des données dans Hadoop plus rapide que le traitement MapReduce traditionnel. Pour les clusters HDInsight de basés sur Windows, il est un moteur facultatif que vous pouvez activer pour la ruche à l’aide de hello commande suivante en tant que partie de votre requête Hive :

    set hive.execution.engine=tez;

Lorsque le travail est soumis tooTez, il crée un dirigées acycliques graphique (DAG) qui décrit l’ordre de hello d’exécution des actions hello requis par le travail de hello. Différentes actions sont appelées des sommets et exécuter une partie de hello travail global. l’exécution réelle de Hello de travail hello décrite par un sommet est appelée une tâche et peut être répartie sur plusieurs nœuds de cluster de hello.

### <a name="understanding-hello-tez-ui"></a>Hello de présentation Tez UI
Hello Tez UI est qu'une page web fournit des informations sur les processus sont en cours d’exécution ou qui ont exécutaient précédemment à l’aide de Tez. Il vous permet de tooview hello DAG généré par Tez, comment elle est répartie entre les clusters, compteurs telles que la mémoire utilisée par les tâches et les sommets et les informations d’erreur. Il offre des informations utiles dans hello les scénarios suivants :

* Surveillance des processus longs, affichage hello la progression de la carte et réduire les tâches.
* Analyse des données historiques pour les processus réussies ou échouées toolearn comment le traitement peut être amélioré ou en raison de l’échec.

## <a name="generate-a-dag"></a>Générer un DAG
Hello Tez UI contiendra uniquement les données si une tâche qui utilise hello Tez moteur est en cours d’exécution ou a été exécuté dans hello passée. Les requêtes Hive simples peuvent généralement être résolues sans utiliser Tez. Toutefois, Tez est généralement nécessaire pour les requêtes plus complexes destinées à filtrer, regrouper, classer, joindre, etc.

Utilisez hello suivant les étapes toorun une requête Hive qui s’exécute à l’aide de Tez.

1. Dans un navigateur web, accédez à toohttps://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** hello désigne votre cluster HDInsight.
2. Dans le menu de hello en hello haut hello, sélectionnez hello **éditeur Hive**. Cela affiche une page avec hello suivant l’exemple de requête.

        Select * from hivesampletable

    Effacer la requête d’exemple hello et remplacez-le par suivant de hello.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. Sélectionnez hello **Submit** bouton. Hello **Session de travail** section bas hello de page de hello affichera hello de requête de hello. Une fois hello les changements d’état trop**terminé**, sélectionnez hello **afficher les détails** lier tooview hello résultats. Hello **sortie des tâches** sont similaires toohello suivants :

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>Utilisez hello Tez UI
> [!NOTE]
> Hello Tez UI est uniquement disponible à partir du bureau hello hello principal des nœuds de cluster, vous devez utiliser les nœuds principaux de toohello tooconnect Bureau à distance.
>
>

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre cluster HDInsight. À partir du haut hello du Panneau de HDInsight hello, sélectionnez hello **Bureau à distance** icône. Panneau de bureau à distance hello s’affiche

    ![Icône Bureau à distance](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. Dans le panneau de bureau à distance hello, sélectionnez **Connect** nœud principal du cluster toohello tooconnect. Lorsque vous y êtes invité, utilisez hello cluster connexion Bureau à distance utilisateur nom et mot de passe tooauthenticate hello.

    ![Icône Connexion Bureau à distance](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > Si vous n’avez pas activé la connectivité Bureau à distance, fournissez un nom d’utilisateur, le mot de passe et la date d’expiration, puis sélectionnez **activer** tooenable Bureau à distance. Une fois qu’elle a été activée, utilisez hello précédentes étapes tooconnect.
   >
   >
3. Une fois connecté, ouvrez Internet Explorer sur le Bureau à distance hello, icône d’engrenage sélectionnez hello dans hello coin supérieur droit navigateur hello, puis **paramètres d’affichage de compatibilité**.
4. À partir du bas hello de **paramètres d’affichage de compatibilité**, désactivez hello case à cocher **afficher les sites intranet dans Affichage de compatibilité** et **listes de compatibilité d’utiliser Microsoft**, puis sélectionnez **fermer**.
5. Dans Internet Explorer, accédez à toohttp://headnodehost:8188/tezui / #. Cette action affiche hello Tez UI

    ![Interface utilisateur Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    Lors du chargement de hello Tez UI, vous verrez une liste de décisionnels qui sont en cours d’exécution, ou qui ont été exécutés sur le cluster de hello. affichage par défaut de Hello inclut Bonjour Dag Name, Id, émetteur, état, l’heure de début, heure de fin, durée, ID d’Application et file d’attente. Plus de colonnes peuvent être ajoutés à l’aide d’icône d’engrenage hello en hello à droite de la page de hello.

    Si vous avez une seule entrée, il sera de requête hello que vous avez exécuté dans la section précédente de hello. Si vous avez plusieurs entrées, vous pouvez rechercher en entrant les critères de recherche dans les champs hello ci-dessus hello décisionnels, puis appuyez sur **entrée**.
6. Sélectionnez hello **Dag Name** pour l’entrée de DAG hello plus récente. Cela affiche des informations sur hello DAG, ainsi que toodownload d’option hello un fichier zip de fichiers JSON qui contiennent des informations sur hello DAG.

    ![Détails du DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Ci-dessus hello **DAG détails** plusieurs liens qui peuvent être utilisés toodisplay informations hello DAG.

   * **Compteurs du DAG** permet d’afficher les informations de compteurs pour ce DAG.
   * **Vue graphique** permet d’afficher une représentation graphique de ce DAG.
   * **Tous les sommets** affiche une liste des sommets de hello dans cet DAG.
   * **Toutes les tâches** affiche une liste de tâches hello pour tous les sommets dans cet DAG.
   * **Tous les TaskAttempts** affiche des informations sur hello tente toorun tâches pour cet DAG.

     > [!NOTE]
     > Si vous faites défiler l’affichage des colonnes hello pour les sommets, tâches et TaskAttempts, notez qu’il existe des liens tooview **compteurs** et **afficher ou télécharger les journaux** pour chaque ligne.
     >
     >

     S’il existe une erreur avec la tâche de hello, hello DAG détails affiche un état Échec, ainsi que de tooinformation de liens sur la tâche ayant échoué hello. Informations de diagnostic seront affichera sous Détails de hello DAG.
8. Sélectionnez **Vue graphique**. Cela affiche une représentation graphique de hello DAG. Vous pouvez placer la souris de hello sur chaque sommet dans hello vue toodisplay informations.

    ![Vue graphique](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. En cliquant sur un sommet chargera hello **détails sommets** pour cet élément. Cliquez sur hello **carte 1** détails toodisplay de sommets pour cet élément. Sélectionnez **confirmer** navigation de hello tooconfirm.

    ![Détails](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Notez que vous disposez maintenant des liens en hello haut hello qui sont des tâches et toovertices connexes.

    > [!NOTE]
    > Vous pouvez également arriver à cette page en revenant trop**DAG détails**, en sélectionnant **détails de sommets**, puis en sélectionnant hello **1 de la carte** sommet.
    >
    >

    * **Compteurs du vertex** permet d’afficher les informations de compteurs pour ce vertex.
    * **Tâches** permet d’afficher les tâches de ce vertex.
    * **Tentatives de tâches** affiche des informations sur les tâches de toorun tentatives pour ce vertex.
    * **Sources et récepteurs** permet d’afficher les sources et les récepteurs de données pour ce vertex.

      > [!NOTE]
      > Comme avec menu précédent de hello, vous pouvez faire défiler l’affichage des colonnes hello pour les tâches, les tentatives de tâche et les Sources & Sinks__ toodisplay lie toomore des informations pour chaque élément.
      >
      >
11. Sélectionnez **tâches**, et puis sélectionnez hello élément **00_000000**. Cette action permet d’afficher les **détails de la tâche**. À partir de cet écran, vous pouvez consulter les **compteurs de tâche** et les **tentatives de tâche**.

    ![Détails de la tâche](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris comment toouse hello Tez afficher, en savoir plus sur [à l’aide de la ruche sur HDInsight](hdinsight-use-hive.md).

Pour plus d’informations techniques sur Tez, consultez hello [page Tez sur Hortonworks](http://hortonworks.com/hadoop/tez/).
