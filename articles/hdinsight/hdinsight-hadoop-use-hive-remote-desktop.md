---
title: "aaaUse Hadoop Hive et Bureau à distance dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment tooconnect tooHadoop cluster HDInsight à l’aide du Bureau à distance, puis exécuter des requêtes Hive à l’aide de hello Hive une Interface de ligne."
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
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>Utilisation de Hive avec Hadoop sur HDInsight via le Bureau à distance
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Dans cet article, vous allez apprendre comment tooconnect tooan HDInsight cluster à l’aide du Bureau à distance, puis exécutez la ruche de requêtes à l’aide de hello Hive d’Interface de ligne de commande (CLI).

> [!IMPORTANT]
> Bureau à distance n’est disponible sur les clusters HDInsight utilisent Windows comme système d’exploitation de hello. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Pour HDInsight 3.4 ou supérieure, consultez [utilisez Hive avec HDInsight et Beeline](hdinsight-hadoop-use-hive-beeline.md) pour plus d’informations sur l’exécution des requêtes Hive directement sur le cluster de hello à partir d’une ligne de commande.

## <a id="prereq"></a>Configuration requise
toocomplete hello étapes décrites dans cet article, vous devez suivant de hello :

* un cluster HDInsight basé sur Windows (Hadoop sur HDInsight)
* Un ordinateur client avec Windows 10, Windows 8 ou Windows 7

## <a id="connect"></a>Connexion avec le Bureau à distance
Activer le Bureau à distance pour le cluster HDInsight de hello, puis connecter tooit en suivant les instructions de hello sur [connecter clusters tooHDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hive"></a>Utilisez la commande de ruche hello
Lorsque vous avez connecté bureau toohello pour le cluster HDInsight de hello, utilisez hello suivant toowork étapes avec Hive :

1. À partir du bureau de HDInsight hello, démarrer hello **ligne de commande Hadoop**.
2. Entrez hello suivant commande toostart hello la ruche de CLI :

        %hive_home%\bin\hive

    Lorsque hello CLI a démarré, vous verrez invite CLI de la ruche de hello : `hive>`.
3. À l’aide de hello CLI, entrez hello suivant les instructions toocreate une nouvelle table nommée **log4jLogs** à l’aide des exemples de données :

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Ces instructions effectuent hello suivant des actions :

   * **DROP TABLE**: supprime la table de hello et le fichier de données hello si hello table existe déjà.
   * **CREATE EXTERNAL TABLE**: crée une table « externe » dans Hive. Tables externes stockent uniquement la définition de table hello dans la ruche (hello données restent dans l’emplacement d’origine de hello).

     > [!NOTE]
     > Tables externes doivent être utilisés lorsque vous attendez hello sous-jacent toobe de données mis à jour par une source externe (par exemple, un processus de téléchargement automatique des données) ou par une autre opération MapReduce, mais souhaitez toujours que ruche interroge les données les plus récentes toouse hello.
     >
     > Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.
     >
     >
   * **FORMAT de ligne**: indique la mise en forme les données de salutation ruche. Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.
   * **EMPLACEMENT du fichier texte comme stockées**: indique la ruche où les données de salutation sont stocké (répertoire de données d’exemple hello) et qu’il est stockée sous forme de texte.
   * **Sélectionnez**: sélectionne un nombre de toutes les lignes où colonne **t4** contient la valeur de hello **[erreur]**. Cette commande renvoie la valeur **3** , car trois lignes contiennent cette valeur.
   * **INPUT__FILE__NAME LIKE '%.log'** : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log. Cela limite hello recherche toohello exemple.log fichier qui contient les données de salutation et empêche de renvoi de données à partir de l’autre exemple de fichiers de données qui ne correspondent pas aux schéma hello que nous avons défini.
4. Hello utilisation suivant les instructions toocreate une nouvelle table « interne » nommée **journaux d’erreurs de**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    Ces instructions effectuent hello suivant des actions :

   * **CREATE TABLE IF NOT EXISTS**: crée une table, le cas échéant. Étant donné que hello **externe** mot clé n’est pas utilisé, il s’agit d’une table interne, qui est stockée dans l’entrepôt de données Hive hello et entièrement gérée par ruche.

     > [!NOTE]
     > Contrairement aux **externe** supprime les tables, suppression d’une table interne également hello les données sous-jacentes.
     >
     >
   * **STOCKÉES des ORC AS**: stocke les données de hello ligne optimisé (ORC) sous forme de colonnes. Il s'agit d'un format particulièrement efficace et optimisé pour le stockage de données Hive.
   * **INSERT OVERWRITE ... Sélectionnez**: sélectionne des lignes à partir de hello **log4jLogs** table qui contiennent des **[erreur]**, puis insère hello des données dans hello **journaux d’erreurs de** table.

     tooverify que seules les lignes qui contiennent **[erreur]** dans la colonne t4 étaient stockée toohello **journaux d’erreurs** table, utilisez hello suivant tooreturn instruction tous hello des lignes à partir de **journaux d’erreurs de**:

       SELECT * from errorLogs;

     Trois lignes de données doivent normalement être renvoyées. Elles contiennent toutes **[ERROR]** dans la colonne t4.

## <a id="summary"></a>Résumé
Comme vous pouvez le voir, Bonjour Bonjour ruche commande fournit une toointeractively facilement exécuter des requêtes Hive sur un cluster HDInsight, hello d’analyse état du travail et d’extraire la sortie de hello.

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
