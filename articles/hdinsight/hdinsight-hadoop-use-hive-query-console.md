---
title: "aaaUse Hadoop Hive sur hello Console de requête dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello basée sur le web Console de requête toorun requêtes Hive sur un HDInsight Hadoop de cluster à partir de votre navigateur."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a>Exécuter des requêtes Hive à l’aide de la Console de requête de hello
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Dans cet article, vous allez apprendre comment les requêtes toouse hello Console de requête HDInsight toorun Hive sur un HDInsight Hadoop cluster depuis votre navigateur.

> [!IMPORTANT]
> Hello Console de requête HDInsight est disponible uniquement sur les clusters HDInsight de basés sur Windows. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Pour HDInsight 3.4 ou version supérieure, consultez [Run Hive queries in Ambari Hive View (Exécution de requêtes Hive dans la vue Hive d’Ambari)](hdinsight-hadoop-use-hive-ambari-view.md) pour plus d’informations sur l’exécution de requêtes Hive à partir d’un navigateur web.

## <a id="prereq"></a>Configuration requise
toocomplete hello étapes décrites dans cet article, vous devez suivant de hello.

* Un cluster Hadoop HDInsight Windows
* Un navigateur Web moderne

## <a id="run"></a>Exécuter des requêtes Hive à l’aide de la Console de requête de hello
1. Ouvrez un navigateur web et accédez trop**https://CLUSTERNAME.azurehdinsight.net**, où **CLUSTERNAME** hello désigne votre cluster HDInsight. Si vous y êtes invité, entrez le nom d’utilisateur hello et un mot de passe que vous avez utilisé lors de la création de cluster de hello.
2. À partir des liens de hello en hello haut hello, sélectionnez **éditeur Hive**. Cela affiche un formulaire qui peut être utilisé tooenter hello HiveQL instructions que vous souhaitez toorun dans le cluster HDInsight de hello.

    ![éditeur de ruche Hello](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    Remplacez le texte hello `Select * from hivesampletable` avec hello suivant les instructions HiveQL :

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Ces instructions effectuent hello suivant des actions :

   * **DROP TABLE**: supprime la table de hello et le fichier de données hello si hello table existe déjà.
   * **CREATE EXTERNAL TABLE**: crée une table « externe » dans Hive. Tables externes stockent uniquement la définition de table hello dans la ruche ; les données de salutation reste dans l’emplacement d’origine de hello.

     > [!NOTE]
     > Tables externes doivent être utilisés lorsque vous attendez hello sous-jacent toobe de données mis à jour par une source externe (par exemple, un processus de téléchargement automatique des données) ou par une autre opération MapReduce, mais souhaitez toujours que ruche interroge les données les plus récentes toouse hello.
     >
     > Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.
     >
     >
   * **FORMAT de ligne**: indique la mise en forme les données de salutation ruche. Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.
   * **EMPLACEMENT du fichier texte comme stockées**: indique la ruche où les données de salutation sont stocké (répertoire de données d’exemple hello) et qu’il est stockée sous forme de texte
   * **Sélectionnez**: sélectionnez un nombre de toutes les lignes où colonne **t4** contiennent la valeur de hello **[erreur]**. Cette commande renvoie la valeur **3** , car trois lignes contiennent cette valeur.
   * **INPUT__FILE__NAME LIKE '%.log'** : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log. Cela limite hello recherche toohello exemple.log fichier qui contient les données de salutation et empêche de renvoi de données à partir de l’autre exemple de fichiers de données qui ne correspondent pas aux schéma hello que nous avons défini.
3. Cliquez sur **Envoyer**. Hello **Session de travail** à hello en bas de page de hello doit afficher les détails de tâche de hello.
4. Hello lorsque **état** champ change trop**terminé**, sélectionnez **afficher les détails** pour le travail de hello. Sur la page de détails de hello, hello **sortie des tâches** contient `[ERROR]    3`. Vous pouvez utiliser hello **télécharger** bouton sous cette toodownload de champ d’un fichier qui contient la sortie de hello du travail de hello.

## <a id="summary"></a>Résumé
Comme vous pouvez le voir, hello Console de requête fournit un moyen simple de toorun ruche les requêtes dans un cluster HDInsight, surveiller l’état de la tâche hello et récupérer la sortie de hello.

toolearn savoir plus sur l’aide de tâches de Console de requête Hive toorun Hive, sélectionnez **mise en route** haut hello de hello Console de requête, puis utiliser les exemples hello fournis. Chaque exemple de guide de processus de hello d’à l’aide de la ruche tooanalyze données, y compris des explications sur les instructions HiveQL hello utilisées dans l’exemple hello.

## <a id="nextsteps"></a>Étapes suivantes
Pour obtenir des informations générales sur Hive dans HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

Si vous utilisez Tez avec Hive, consultez hello suivant des documents pour les informations de débogage :

* [Utilisez hello Tez UI sur HDInsight de basés sur Windows](hdinsight-debug-tez-ui.md)
* [Utilisez hello vue Ambari Tez sur HDInsight de basés sur Linux](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
