---
title: "Utiliser Hadoop Hive et le Bureau à distance dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment vous connecter à un cluster Hadoop à l'aide du Bureau à distance, et exécuter ensuite des requêtes Hive à l'aide de l'interface de ligne de commande (CLI) Hive."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: ded90b0f94e545b4066a0220afffae26f1cd15ee
ms.sourcegitcommit: f8437edf5de144b40aed00af5c52a20e35d10ba1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>Utilisation de Hive avec Hadoop sur HDInsight via le Bureau à distance
[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

Dans cet article, vous découvrirez comment vous connecter à un cluster HDInsight à l'aide du Bureau à distance, et exécuter ensuite des requêtes Hive à l'aide de l'interface de ligne de commande (CLI) Hive.

> [!IMPORTANT]
> Le Bureau à distance n’est disponible que sur les clusters HDInsight qui utilisent Windows comme système d’exploitation. Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Pour HDInsight 3.4 ou les versions supérieures, consultez l’article [Utilisation de Hive avec Hadoop dans HDInsight via Beeline](apache-hadoop-use-hive-beeline.md) pour plus d’informations sur l’exécution de requêtes Hive directement sur le cluster à partir d’une ligne de commande.

## <a id="prereq"></a>Configuration requise
Pour effectuer les étapes présentées dans cet article, vous avez besoin des éléments suivants :

* un cluster HDInsight basé sur Windows (Hadoop sur HDInsight)
* Un ordinateur client avec Windows 10, Windows 8 ou Windows 7

## <a id="connect"></a>Connexion avec le Bureau à distance
Activez le Bureau à distance pour le cluster HDInsight, puis connectez-vous à lui en suivant les instructions fournies dans [Connexion à des clusters HDInsight avec RDP](../hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hive"></a>Utilisation de la commande Hive
Une fois connecté au bureau pour le cluster HDInsight, effectuez les étapes suivantes pour utiliser Hive.

1. À partir du bureau HDInsight, démarrez la **ligne de commande Hadoop**.
2. Exécutez la commande suivante pour démarrer l'interface de ligne de commande (CLI) Hive :

        %hive_home%\bin\hive

    Une fois l'interface de ligne de commande lancée, vous verrez apparaître l'invite CLI : `hive>`.
3. En utilisant l'interface de ligne de commande, saisissez les instructions suivantes pour créer une table nommée **log4jLogs** à l'aide d'exemples de données :

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Ces instructions effectuent les opérations suivantes :

   * **DROP TABLE**: supprime la table et le fichier de données, si la table existe déjà.
   * **CREATE EXTERNAL TABLE**: crée une table externe dans Hive. Les tables externes stockent uniquement la définition de table dans Hive (les données restent à leur emplacement d’origine).

     > [!NOTE]
     > Les tables externes doivent être utilisées lorsque vous vous attendez à ce que les données sous-jacentes soient mises à jour par une source externe (comme un processus de téléchargement de données automatisé) ou par une autre opération MapReduce, mais souhaitez toujours que les requêtes Hive utilisent les données les plus récentes.
     >
     > La suppression d'une table externe ne supprime **pas** les données, mais seulement la définition de la table.
     >
     >
   * **ROW FORMAT**: indique à Hive le mode de formatage des données. Dans ce cas, les champs de chaque journal sont séparés par un espace.
   * **STORED AS TEXTFILE LOCATION**: indique à Hive l'emplacement des données (le répertoire exemple/données) et précise qu'elles sont stockées sous la forme de texte.
   * **SELECT** : sélectionne toutes les lignes dont la colonne **t4** contient la valeur **[ERROR]**. Cette commande renvoie la valeur **3** , car trois lignes contiennent cette valeur.
   * **INPUT__FILE__NAME LIKE '%.log'** : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log. Cela limite la recherche au fichier sample.log qui contient les données et l'empêche de renvoyer des données provenant d'autres fichiers d'exemple qui ne correspondent pas au schéma que nous avons défini.
4. Utilisez les instructions suivantes pour créer une table « interne » nommée **errorLogs**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    Ces instructions effectuent les opérations suivantes :

   * **CREATE TABLE IF NOT EXISTS**: crée une table, le cas échéant. Le mot-clé **EXTERNAL** n’étant pas utilisé, il s’agit d’une table interne, stockée dans l’entrepôt de données Hive et gérée intégralement par Hive.

     > [!NOTE]
     > Contrairement aux tables **EXTERNES** , la suppression d’une table interne entraîne également la suppression des données sous-jacentes.
     >
     >
   * **STORED AS ORC**: stocke les données au format ORC (Optimized Row Columnar). Il s'agit d'un format particulièrement efficace et optimisé pour le stockage de données Hive.
   * **INSERT OVERWRITE ... SELECT** : sélectionne des lignes de la table **log4jLogs** qui contiennent **[ERROR]**, puis insère les données dans la table **errorLogs**.

     Pour vérifier que seules les lignes contenant **[ERROR]** dans la colonne t4 ont été stockées dans la table **errorLogs**, utilisez l’instruction suivante afin de renvoyer toutes les lignes à partir de **errorLogs** :

       SELECT * from errorLogs;

     Trois lignes de données doivent normalement être renvoyées. Elles contiennent toutes **[ERROR]** dans la colonne t4.

## <a id="summary"></a>Résumé
Comme vous pouvez le constater, la commande Hive permet d'exécuter facilement, et de façon interactive, des requêtes Hive sur un cluster HDInsight, de surveiller l'état de la tâche et de récupérer le résultat.

## <a id="nextsteps"></a>Étapes suivantes
Pour obtenir des informations générales sur Hive dans HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

Si vous utilisez Tez avec Hive, consultez les documents suivants pour les informations de débogage :

* [Utiliser l'interface utilisateur Tez sur HDInsight Windows](../hdinsight-debug-tez-ui.md)
* [Utilisez la vue Tez Ambari sur HDInsight Linux](../hdinsight-debug-ambari-tez-view.md)

[1]:apache-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
