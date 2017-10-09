---
title: aaaWhat est Apache Hive et HiveQL - Azure HDInsight | Documents Microsoft
description: "Apache Hive est un système d’entrepôt de données pour Hadoop. Vous pouvez interroger les données stockées dans la ruche à l’aide de HiveQL, tooTransact-SQL similaire. Dans ce document, vous devez savoir comment la ruche toouse et HiveQL avec Azure HDInsight."
keywords: "hiveql, quelle est la ruche, hadoop hiveql, comment toouse hive, découvrez hive, quelle est la ruche"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>Présentation d’Apache Hive et HiveQL sur Azure HDInsight

[Apache Hive](http://hive.apache.org/) est un système d’entrepôt de données pour Hadoop. Hive permet la synthèse, l’interrogation et l’analyse des données. Requêtes Hive sont écrites dans HiveQL, qui est un tooSQL similaire de langage de requête.

Ruche vous permet de tooproject structure sur des données en grande partie non structurées. Après avoir défini la structure de hello, vous pouvez utiliser les données de salutation HiveQL tooquery sans avoir connaissance de Java ou MapReduce.

HDInsight fournit plusieurs types de cluster adaptés à des charges de travail spécifiques. Hello cluster types suivants est souvent utilisée pour les requêtes Hive :

* __Ruche interactif__: cluster Hadoop de A qui fournit [faible latence analytiques de traitement (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) temps de réponse de tooimprove de fonctionnalités des requêtes interactives. Pour plus d’informations, consultez hello [démarrer avec la ruche Interactive dans HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.

* __Hadoop__ : cluster Hadoop adapté aux charges de travail de traitement par lots. Pour plus d’informations, consultez hello [démarrer avec Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.

* __Spark__ : Apache Spark intègre une fonctionnalité permettant de travailler avec Hive. Pour plus d’informations, consultez hello [démarrer avec Spark sur HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.

* __HBase__: HiveQL peut être tooquery utilisé les données stockées dans HBase. Pour plus d’informations, consultez hello [démarrer avec HBase sur HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.

## <a name="how-toouse-hive"></a>Comment la ruche toouse

Utilisez hello suivant toodiscover table comment toouse Hive hdinsight :

| **Utilisez cette méthode** si vous souhaitez... | ... un interpréteur de commandes **interactif** | ... un traitement par **lots** | ...avec ce **système d’exploitation cluster** | ...depuis ce **système d’exploitation cluster** |
|:--- |:---:|:---:|:--- |:--- |
| [Affichage Hive](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |N’importe lequel (basé sur le navigateur) |
| [Client Beeline](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X ou Windows |
| [API REST](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux ou Windows* |Linux, Unix, Mac OS X ou Windows |
| [Outils HDInsight pour Visual Studio](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux ou Windows* |Windows |
| [Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux ou Windows* |Windows |

> [!IMPORTANT]
> \*Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Si vous utilisez un cluster HDInsight de basés sur Windows, vous pouvez utiliser hello [console de requête](hdinsight-hadoop-use-hive-query-console.md) depuis votre navigateur ou [Bureau à distance](hdinsight-hadoop-use-hive-remote-desktop.md) toorun des requêtes Hive.

## <a name="hiveql-language-reference"></a>Référence du langage HiveQL

Référence du langage HiveQL est disponible dans hello [manuel de langage (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).

## <a name="hive-and-data-structure"></a>Hive et structure des données

Ruche comprend des données semi-structurées et structuration de toowork avec. Par exemple, fichiers texte dans lequel les champs de hello sont délimités par des caractères spécifiques. Hello HiveQL instruction qui suit crée une table sur délimitées par un espace de données :

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

Hive prend également en charge un **sérialiseur/ désérialiseur (SerDe)** personnalisé pour des données structurées de manière irrégulière ou complexes. Pour plus d’informations, consultez hello [comment toouse un SerDe JSON personnalisée avec HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.

Pour plus d’informations sur les formats de fichier pris en charge par la ruche, consultez hello [manuel de langage (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>Tables internes et externes Hive

Hive vous permet de créer deux types de tables :

* __Interne__: données sont stockées dans l’entrepôt de données Hive hello. Hello l’entrepôt de données se trouve dans `/hive/warehouse/` sur le stockage par défaut hello pour le cluster de hello.

    Utilisez des tables internes quand :

    * les données sont temporaires.
    * Vous souhaitez ruche toomanage hello du cycle de vie de la table de hello et données.

* __Externe__: les données sont stockées en dehors de l’entrepôt de données hello. les données de salutation pouvant figurer sur n’importe quel stockage accessible par cluster de hello.

    Utilisez des tables externes quand :

    * les données de salutation sont également utilisées en dehors de la ruche. Par exemple, les fichiers de données hello sont mis à jour par un autre processus (qui ne verrouille pas les fichiers hello.)
    * Les données doivent tooremain Bonjour sous-jacent emplacement, même après la suppression de table de hello.
    * Vous avez besoin d’un emplacement personnalisé, par exemple un compte de stockage non sélectionné par défaut.
    * Un programme autre que ruche gère le format de données hello, l’emplacement, etc..

Pour plus d’informations, consultez hello [Hive interne et externe Tables Intro] [ cindygross-hive-tables] billet de blog.

## <a name="user-defined-functions-udf"></a>Fonctions définies par l’utilisateur (UDF)

Hive peut également être étendu via des **fonctions définies par l'utilisateur (UDF)**. Un fichier UDF vous permet de tooimplement de fonctionnalité ou logique qui n’est pas facilement être modelée dans HiveQL. Pour obtenir un exemple d’utilisation des UDF avec Hive, consultez hello suivant des documents :

* [Utiliser une fonction Java définie par l’utilisateur avec Hive](hdinsight-hadoop-hive-java-udf.md)

* [Utiliser une fonction Python définie par l’utilisateur avec Hive et Pig](hdinsight-python.md)

* [Utiliser une fonction C# définie par l’utilisateur avec Hive et Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Fonctionnement des tooHDInsight tooadd une ruche personnalisée défini par l’utilisateur](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [Une date/heure exemple ruche fonction définie par l’utilisateur tooconvert met en forme tooHive timestamp](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>Exemple de données

Hive sur HDInsight est préchargé avec une table interne nommée `hivesampletable`. HDInsight fournit également des exemples de jeux de données pouvant être utilisés avec Hive. Ces jeux de données sont stockées dans hello `/example/data` et `/HdiSamples` répertoires. Ils existent dans le stockage par défaut hello pour votre cluster.

## <a id="job"></a>Exemple de requête Hive

Hello suivant des colonnes de projet instructions HiveQL sur hello `/example/data/sample.log` fichier :

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

Dans l’exemple précédent de hello, les instructions HiveQL hello effectuent hello suivant des actions :

* `set hive.execution.engine=tez;`: Jeux hello toouse du moteur d’exécution Tez. L’utilisation de Tez au lieu de MapReduce peut augmenter les performances de requête. Pour plus d’informations sur Tez, consultez hello [Tez d’Apache utilisation pour améliorer les performances](#usetez) section.

    > [!NOTE]
    > Cette instruction est uniquement requise lorsque vous utilisez un cluster HDInsight sous Windows. Tez est le moteur d’exécution par défaut hello pour HDInsight de basés sur Linux.

* `DROP TABLE`: Si la table de hello existe déjà, supprimez-le.

* `CREATE EXTERNAL TABLE` : crée une table **externe** dans Hive. Les tables externes ne stockent la définition de table hello Hive. les données de salutation reste dans l’emplacement d’origine de hello et au format d’origine de hello.

* `ROW FORMAT`: Indique la ruche de mise en forme les données de salutation. Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.

* `STORED AS TEXTFILE LOCATION`: Indique ruche où hello les données sont stockées (hello `example/data` active) et qu’il est stocké sous forme de texte. les données de salutation peuvent être dans un fichier ou réparties sur plusieurs fichiers dans le répertoire de hello.

* `SELECT`: Sélectionne un nombre de toutes les lignes où hello colonne **t4** contient la valeur de hello **[erreur]**. Cette instruction renvoie la valeur **3**, car trois lignes contiennent cette valeur.

* `INPUT__FILE__NAME LIKE '%.log'`-Ruche tente de fichiers de tooall tooapply hello schéma dans le répertoire de hello. Dans ce cas, le répertoire de hello contient des fichiers qui ne correspondent pas hello schéma. données de garbage tooprevent dans les résultats de hello, cette instruction indique ruche que nous devons retourner uniquement les données à partir de fichiers se terminant par. journal.

> [!NOTE]
> Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe. Par exemple, un processus de chargement de données automatisé ou une opération MapReduce.
>
> Suppression d’une table externe est **pas** supprimer les données de salutation, elle supprime uniquement la définition de la table hello.

toocreate un **interne** table externe à la place, utilisez hello suivant HiveQL :

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

Ces instructions effectuent hello suivant des actions :

* `CREATE TABLE IF NOT EXISTS`: Si la table de hello n’existe pas, créez-le. Étant donné que hello **externe** mot clé n’est pas utilisé, cette instruction crée une table interne. tableau de Hello est stocké dans l’entrepôt de données Hive hello et entièrement géré par ruche.

* `STORED AS ORC`: Stocke les données de hello dans format optimisé lignes en colonnes (ORC). ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.

* `INSERT OVERWRITE ... SELECT`: Sélectionne des lignes à partir de hello **log4jLogs** table qui contient **[erreur]**, et puis insertions hello des données dans hello **journaux d’erreurs de** table.

> [!NOTE]
> Contrairement aux tables externes, la suppression d’une table interne supprime également les données sous-jacentes hello.

## <a name="improve-hive-query-performance"></a>Améliorer les performances des requêtes Hive

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org) est une infrastructure qui permet à des applications utilisant beaucoup de données, tels que Hive, toorun beaucoup plus efficacement à l’échelle. Tez est activé par défaut pour les clusters HDInsight basés sur Linux.

> [!NOTE]
> Tez est actuellement désactivé par défaut pour les clusters HDInsight basés sur Windows, et il doit être activé. avantage tootake de Tez, hello valeur suivante doit être définie pour une requête Hive :
>
> `set hive.execution.engine=tez;`
>
> Tez est moteur par défaut de hello pour les clusters HDInsight de basés sur Linux.

Hello [Hive sur les documents de conception Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contient des détails sur le choix d’implémentation hello et les configurations de paramétrage.

tooaid dans les tâches de débogage exécuté à l’aide de Tez, HDInsight fournit hello suivant des interfaces utilisateur web qui vous permettre de tooview les détails des travaux de Tez :

* [Utilisez hello vue Ambari Tez sur HDInsight de basés sur Linux](hdinsight-debug-ambari-tez-view.md)

* [Utilisez hello Tez UI sur HDInsight de basés sur Windows](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>Low Latency Analytical Processing (LLAP)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (parfois appelé Live Long and Process) est une nouvelle fonctionnalité de Hive 2.0 qui permet la mise en cache en mémoire des requêtes. LLAP effectue des requêtes Hive beaucoup plus rapides des trop[26 x plus rapide que la ruche 1.x dans certains cas](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).

HDInsight fournit LLAP Bonjour Hive interactif de type de cluster. Pour plus d’informations, consultez hello [démarrer avec la ruche interactif](hdinsight-hadoop-use-interactive-hive.md) document.

## <a name="hive-jobs-and-sql-server-integration-services"></a>Tâches Hive et SQL Server Integration Services

Vous pouvez utiliser SQL Server Integration Services (SSIS) toorun un travail Hive. Bonjour Azure Feature Pack pour SSIS fournit hello suivant des composants qui fonctionnent avec les tâches Hive dans HDInsight.

* [Tâche Hive d’Azure HDInsight][hivetask]

* [Gestionnaire de connexions d’abonnement Azure][connectionmanager]

En savoir plus sur hello Azure Feature Pack pour SSIS [ici][ssispack].

## <a id="nextsteps"></a>Étapes suivantes

Maintenant que vous savez quelle est la ruche et comment toouse avec Hadoop dans HDInsight, hello utilisation suivant lie tooexplore autres toowork manières avec Azure HDInsight.

* [Télécharger des données tooHDInsight][hdinsight-upload-data]
* [Utilisation de Pig avec HDInsight][hdinsight-use-pig]
* [Utilisation des tâches MapReduce avec HDInsight][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
