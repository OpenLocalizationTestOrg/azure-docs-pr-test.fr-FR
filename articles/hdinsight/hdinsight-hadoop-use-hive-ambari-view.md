---
title: toowork de vues de Ambari aaaUse avec Hive dans HDInsight (Hadoop) - Azure | Documents Microsoft
description: "Découvrez comment toouse hello Hive une vue à partir de vos requêtes de ruche de toosubmit de navigateur web. Hello, vue de la ruche fait partie de hello que l’interface utilisateur de Ambari Web fourni avec votre cluster HDInsight de basés sur Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a>Utilisez hello Hive une vue avec Hadoop dans HDInsight

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Découvrez comment toorun ruche interroge l’affichage de la ruche Ambari. Ambari est un utilitaire de gestion et de surveillance fourni avec les clusters HDInsight sous Linux. Une des fonctionnalités hello fournies via Ambari est une interface utilisateur Web qui peuvent être des requêtes de ruche toorun utilisé.

> [!NOTE]
> Ambari offre de nombreuses fonctionnalités qui ne sont pas traitées dans ce document. Pour plus d’informations, consultez [HDInsight de gérer des clusters à l’aide de hello l’interface utilisateur de Ambari Web](hdinsight-hadoop-manage-ambari.md).

## <a name="prerequisites"></a>Composants requis

* Un cluster HDInsight sous Linux Pour plus d’informations sur la création d’un cluster, consultez [Prise en main de HDInsight sous Linux](hdinsight-hadoop-linux-tutorial-get-started.md).

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="open-hello-hive-view"></a>Afficher la ruche hello

Vous pouvez les vues Ambari de hello portail Azure ; Sélectionnez votre cluster HDInsight, puis **Ambari vues** de hello **liens rapides** section.

![section des liens rapides du portail de hello](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

Dans la liste hello des vues, sélectionnez hello __affichage de la ruche__.

![Hello vue ruche sélectionnée](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> Lors de l’accès Ambari, vous êtes invité à tooauthenticate toohello site. Entrez hello admin (valeur par défaut `admin`) compte nom et mot de passe utilisé lors de la création de cluster hello.

Vous devez voir un toohello similaire de page suivant l’image :

![Image de la feuille de calcul hello requête de vue de ruche hello](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>Exécuter une requête

toorun une requête hive, utilisez hello comme suit à partir de la vue de ruche hello.

1. À partir de hello __requête__ onglet, collez hello suivant les instructions HiveQL dans la feuille de calcul hello :

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    Ces instructions effectuent hello suivant des actions :

   * `DROP TABLE`-Supprime la table de hello et fichier de données hello, au cas où la table hello existe déjà.

   * `CREATE EXTERNAL TABLE` : crée une nouvelle table « externe » dans Hive.
   Tables externes stockent uniquement la définition de table hello dans la ruche. les données de salutation reste dans l’emplacement d’origine de hello.

   * `ROW FORMAT`-Comment les données de salutation sont mis en forme. Dans ce cas, les champs de hello dans chaque journal sont séparés par un espace.

   * `STORED AS TEXTFILE LOCATION`-Où sont stockées les données de hello et qu’elle est stockée sous forme de texte.

   * `SELECT`-Sélectionne un nombre de toutes les lignes où t4 de colonne contient la valeur de hello [erreur].

     > [!NOTE]
     > Tables externes doivent être utilisées lorsque vous attendez hello toobe de données sous-jacent mis à jour par une source externe. par exemple, par un processus de téléchargement de données automatisé ou une autre opération MapReduce. Suppression d’une table externe est *pas* supprimer les données de hello, uniquement la définition de table hello.

    > [!IMPORTANT]
    > Laissez hello __base de données__ sélection à __par défaut__. des exemples de Hello dans ce document utilisent la base de données par défaut hello inclus avec HDInsight.

2. requête de hello toostart, utilisez hello **Execute** situé sous la feuille de calcul hello. Il désactive les modifications de texte orange et hello trop**arrêter**.

3. Une fois la requête hello est terminée, hello **résultats** onglet affiche les résultats de hello de hello. Hello suivant le texte est résultat hello de requête de hello :

        sev       cnt
        [ERROR]   3

    Hello **journaux** onglet peut être des informations de journalisation utilisé tooview hello créées par le travail de hello.

   > [!TIP]
   > Hello **enregistrer les résultats** liste déroulante de boîte de dialogue de hello supérieur gauche de hello **résultats du processus de requête** section vous permet de toodownload ou enregistrer les résultats.

4. Sélectionnez hello quatre premières lignes de cette requête, puis sélectionnez **Execute**. Notez qu’il n’y a aucun résultat hello travail une fois. À l’aide de hello **Execute** bouton lorsqu’il fait partie de la requête de hello est sélectionné uniquement s’exécute hello instructions sélectionnées. Dans ce cas, la sélection hello n’inclure hello dernière instruction qui extrait des lignes de table de hello. Si vous sélectionnez uniquement cette ligne et utilisez **Execute**, vous devez voir les résultats de hello attendu.

5. tooadd une feuille de calcul, utilisez hello **nouvelle feuille de calcul** bouton bas hello hello **l’éditeur de requête**. Dans hello nouvelle feuille de calcul, entrez hello suivant les instructions HiveQL :

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  Ces instructions effectuent hello suivant des actions :

   * **CREATE TABLE IF NOT EXISTS** : crée une table, si elle n'existe pas déjà. Depuis hello **externe** mot clé n’est pas utilisé, une table interne est créée. Une table interne est stockée dans l’entrepôt de données Hive hello et entièrement gérée par ruche. Contrairement aux tables externes, la suppression d’une table interne supprime également des données sous-jacentes hello.

   * **ORC de AS stockées** -stocke les données de hello dans format optimisé lignes en colonnes (ORC). ORC est un format particulièrement efficace et optimisé pour le stockage de données Hive.

   * **INSERT OVERWRITE ... Sélectionnez** -sélectionne des lignes à partir de hello **log4jLogs** table qui contiennent des `[ERROR]`, et puis insertions hello des données dans hello **journaux d’erreurs de** table.

     Hello d’utilisation **Execute** bouton toorun cette requête. Hello **résultats** onglet ne contient pas d’informations lors de la requête de hello retourne zéro ligne. état de Hello doit être **SUCCEEDED** une fois la requête de hello terminée.

### <a name="visual-explain"></a>Visual Explain

toodisplay une visualisation hello du plan de requête, sélectionnez hello **expliquent Visual** onglet au-dessous de feuille de calcul hello.

Hello **expliquent Visual** vue de requête de hello peut être utile de comprendre le flux hello de requêtes complexes. Vous pouvez afficher un équivalent textuel de cette vue à l’aide de hello **expliquer** bouton Bonjour éditeur de requête.

### <a name="tez-ui"></a>Interface utilisateur Tez

toodisplay hello Tez UI pour requête hello, sélectionnez hello **Tez** onglet au-dessous de feuille de calcul hello.

> [!IMPORTANT]
> Tez est tooresolve non utilisé toutes les requêtes. De nombreuses requêtes peuvent être résolues sans utiliser Tez. 

Si Tez était une requête de hello tooresolve utilisé, hello graphique acyclique dirigé (DAG) s’affiche. Si vous souhaitez tooview hello DAG pour les requêtes, vous avez exécuté Bonjour passées ou déboguez hello Tez processus, utilisez hello [Tez vue](hdinsight-debug-ambari-tez-view.md) à la place.

## <a name="view-job-history"></a>Afficher l’historique des tâches

Hello __travaux__ onglet affiche un historique des requêtes Hive.

![Image de l’historique des travaux hello](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>Tables de base de données

Vous pouvez utiliser hello __Tables__ onglet toowork avec des tables dans une base de données de la ruche.

![Image de l’onglet de tables hello](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>Requêtes enregistrées

À partir de l’onglet de requête hello, vous pouvez éventuellement enregistrer des requêtes. Une fois enregistré, vous pouvez réutiliser des requêtes hello de hello __requêtes enregistrées__ onglet.

![Image de l’onglet de requêtes enregistrées](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>Fonctions définies par l’utilisateur

Hive peut également être étendu via des fonctions définies par l'utilisateur (UDF). Un fichier UDF vous permet de tooimplement de fonctionnalité ou logique qui n’est pas facilement être modelée dans HiveQL.

Hello onglet UDF haut hello hello la ruche de vue vous permet de toodeclare et enregistrer des UDF. Ces fonctions UDF peuvent être utilisés avec hello **l’éditeur de requête**.

![Image de l’onglet UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

Une fois que vous avez ajouté une toohello définie par l’affichage de la ruche, un **insérer UDF** bouton apparaît au bas de hello de hello **l’éditeur de requête**. Cette entrée affiche une liste déroulante de hello UDF définis dans hello vue de la ruche. Sélection d’un fichier UDF ajoute HiveQL instructions tooyour requête tooenable hello UDF.

Par exemple, si vous avez défini une UDF avec hello propriétés suivantes :

* Nom de ressource : myudfs

* Chemin d’accès à la ressource : /myudfs.jar

* Nom de la fonction UDF : myawesomeudf

* Nom de la classe UDF : com.myudfs.Awesome

À l’aide de hello **insérer UDF** bouton affiche une entrée nommée **myudfs**, avec une autre liste déroulante pour chaque UDF défini pour cette ressource. Dans le cas présent, **myawesomeudf**. La sélection de cette entrée ajoute hello suivant début toohello de requête de hello :

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

Vous pouvez ensuite utiliser hello UDF dans votre requête. Par exemple, `SELECT myawesomeudf(name) FROM people;`.

Pour plus d’informations sur l’utilisation des UDF avec Hive dans HDInsight, consultez hello suivant des documents :

* [Utilisation de Python avec Hive et Pig dans HDInsight](hdinsight-python.md)
* [Comment tooadd un tooHDInsight UDF de la ruche personnalisé](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Paramètres Hive

Les paramètres peuvent être utilisé toochange différents paramètres de la ruche. Par exemple, remplaçant moteur d’exécution hello pour la ruche Tez (valeur par défaut de hello) tooMapReduce.

## <a id="nextsteps"></a>Étapes suivantes

Pour obtenir des informations générales sur Hive dans HDInsight.

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)
