---
title: aaaHive avec les outils Data Lake (Hadoop) pour Visual Studio - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse hello Data Lake tools pour Visual Studio les toorun Apache Hive requêtes avec Apache Hadoop sur Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a>Exécuter des requêtes Hive à l’aide des outils de Data Lake hello pour Visual Studio

Découvrez comment toouse hello Data Lake tools pour Visual Studio les tooquery Apache Hive. Hello Data Lake outils permettent de tooeasily créer, soumettre et surveiller tooHadoop des requêtes Hive sur Azure HDInsight.

## <a id="prereq"></a>Configuration requise

* Un cluster Azure HDInsight sous Linux (Hadoop sur HDInsight)

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* (L’une des versions suivantes de hello) de Visual Studio :

    * Visual Studio 2013 Community/Professional/Premium/Ultimate avec mise à jour 4

    * Visual Studio 2015 (toute édition)

    * Visual Studio 2017 (toute édition)

* Outils HDInsight pour Visual Studio ou Outils Azure Data Lake pour Visual Studio. Consultez [prise en main des outils de Visual Studio Hadoop pour HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) pour plus d’informations sur l’installation et configuration des outils de hello.

## <a id="run"></a>Exécuter des requêtes Hive à l’aide de hello Visual Studio

1. Ouvrez **Visual Studio** et sélectionnez **Nouveau** > **Projet** > **Azure Data Lake** > **HIVE** > **Application Hive**. Fournissez un nom pour ce projet.

2. Ouvrez hello **Script.hql** fichier est créé avec ce projet et le coller dans hello suivant les instructions HiveQL :

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    Ces instructions effectuent hello suivant des actions :

   * `DROP TABLE`: Si la table de hello existe, cette instruction supprime.

   * `CREATE EXTERNAL TABLE` : crée une table externe dans Hive. Les tables externes ne stockent la définition de table hello Hive (hello données restent dans l’emplacement d’origine de hello).

     > [!NOTE]
     > Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe. Par exemple, un travail MapReduce ou service Azure.
     >
     > Suppression d’une table externe est **pas** supprimer les données de hello, uniquement la définition de table hello.

   * `ROW FORMAT`: Indique la ruche de mise en forme les données de salutation. Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.

   * `STORED AS TEXTFILE LOCATION`: Indique ruche où hello les données sont stockées (répertoire de données d’exemple hello) et qu’il est stocké sous forme de texte.

   * `SELECT`: Permet de sélectionner un nombre de toutes les lignes où colonne `t4` contient la valeur de hello `[ERROR]`. Cette instruction renvoie la valeur `3`, car trois lignes contiennent cette valeur.

   * `INPUT__FILE__NAME LIKE '%.log'` : indique à Hive de retourner uniquement des données provenant de fichiers se terminant par .log. Cette clause limite hello recherche toohello exemple.log fichier qui contient les données de salutation.

3. Dans la barre d’outils de hello, sélectionnez hello **HDInsight Cluster** que vous souhaitez toouse pour cette requête. Sélectionnez **Submit** toorun les instructions de hello en tant qu’un travail Hive.

   ![Barre d’envoi](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. Hello **récapitulatif de la ruche** apparaît et affiche des informations sur hello travail en cours d’exécution. Hello d’utilisation **Actualiser** lien toorefresh hello informations sur les travaux, jusqu'à ce que hello **état du travail** change également**terminé**.

   ![résumé de tâche affichant un travail terminé](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. Hello d’utilisation **sortie des tâches** lien de sortie de hello tooview de ce travail. Il affiche `[ERROR] 3`, qui est la valeur hello retourné par cette requête.

6. Vous pouvez également exécuter des requêtes Hive sans créer de projet. À l’aide de l’**Explorateur de serveurs**, développez **Azure** > **HDInsight**, cliquez avec le bouton droit sur votre serveur HDInsight, puis sélectionnez **Écrire une requête Hive**.

7. Bonjour **temp.hql** document qui s’affiche, ajoutez hello suivant les instructions HiveQL :

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    Ces instructions effectuent hello suivant des actions :

   * `CREATE TABLE IF NOT EXISTS` : crée une table, si elle n'existe pas déjà. Étant donné que hello `EXTERNAL` mot clé n’est pas utilisé, cette instruction crée une table interne. Tables internes sont stockées dans l’entrepôt de données Hive hello et sont gérés par la ruche.

     > [!NOTE]
     > Contrairement aux `EXTERNAL` supprime les tables, suppression d’une table interne également hello les données sous-jacentes.

   * `STORED AS ORC`: Stocke hello données ligne optimisé (ORC) sous forme de colonnes. ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.

   * `INSERT OVERWRITE ... SELECT`: Sélectionne des lignes à partir de hello `log4jLogs` table qui contiennent des `[ERROR]`, puis insère hello des données dans hello `errorLogs` table.

8. Barre d’outils du hello **Submit** tâche hello de toorun. Hello d’utilisation **état du travail** toodetermine que hello est terminée avec succès.

9. tooverify qui hello travail créé la table hello, utilisez **l’Explorateur de serveurs** et développez **Azure** > **HDInsight** > votre cluster HDInsight > **Bases de données de la ruche** > **par défaut**. Hello **journaux d’erreurs** table et hello **log4jLogs** table sont répertoriés.

## <a id="nextsteps"></a>Étapes suivantes

Comme vous pouvez le voir, hello HDInsight pour Visual Studio garantissent une toowork facilement avec les requêtes Hive dans HDInsight.

Pour obtenir des informations générales sur Hive dans HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)

* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

Pour plus d’informations sur les outils HDInsight hello pour Visual Studio :

* [Prise en main des outils HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
