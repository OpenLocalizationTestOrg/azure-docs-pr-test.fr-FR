---
title: "aaaCreate tables la ruche et charger des données à partir du stockage d’objets Blob Azure | Documents Microsoft"
description: "Créer des tables de la ruche et charger des données dans les tables d’objets blob toohive"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Créer des tables Hive et charger des données à partir de Stockage Blob Azure
Cette rubrique présente des requêtes Hive génériques qui créent des tables Hive et chargent des données à partir d’un stockage d’objets blob Azure. Quelques conseils sont également fourni sur le partitionnement des tables de la ruche et sur l’utilisation de hello optimisées en ligne en colonnes (ORC) mise en forme tooimprove les performances des requêtes.

Cela **menu** lie tootopics qui décrivent comment les données de tooingest dans les environnements cibles où les données de salutation peuvent être stockées et traitées au cours de hello processus de science des données équipe (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez :

* Créé un compte Azure Storage. Pour obtenir des instructions, voir [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).
* Configurer un cluster Hadoop personnalisée avec hello service HDInsight.  Si vous avez besoin d'aide, consultez [Personnaliser des clusters Hadoop Azure HDInsight pour l'analyse avancée](machine-learning-data-science-customize-hadoop-cluster.md).
* Cluster de toohello activé l’accès à distance, connecté et ouvrir la console de ligne de commande Hadoop hello. Si vous avez besoin d’instructions, consultez [hello d’accès nœud principal de Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="upload-data-tooazure-blob-storage"></a>Télécharger le stockage d’objets blob de données tooAzure
Si vous avez créé une machine virtuelle Azure en suivant les instructions hello fournies dans [configurer une machine virtuelle Azure pour analytique avancée](machine-learning-data-science-setup-virtual-machine.md), ce fichier de script doit avoir été téléchargé toohello *C:\\ Les utilisateurs\\\<nom d’utilisateur\>\\Documents\\des Scripts de science des données* répertoire sur l’ordinateur virtuel de hello. Ces requêtes Hive nécessitent uniquement que vous connectez votre propre schéma de données et la configuration du stockage blob Azure dans toobe de champs appropriés hello prêt à envoyer.

Nous partons du principe que les données hello pour les tables de la ruche sont dans un **non compressé** sous forme de tableau, et que les données de salutation a été téléchargé par défaut toohello (ou tooan supplémentaire) conteneur hello du compte de stockage utilisé par le cluster Hadoop de hello.

Si vous souhaitez toopractice sur hello **NYC Taxi voyage données**, vous devez :

* **télécharger** hello 24 [NYC Taxi voyage données](http://www.andresmh.com/nyctaxitrips) fichiers (fichiers de voyage 12 et les fichiers de tarif 12),
* **décompresser** tous les fichiers en fichiers .csv, puis
* **télécharger** les toohello par défaut (ou conteneur approprié) du compte de stockage Azure qui a été créé par la procédure hello hello de hello [personnaliser Azure HDInsight Hadoop pour le processus d’Analytique avancée et la technologie des clusters ](machine-learning-data-science-customize-hadoop-cluster.md) rubrique. Hello processus tooupload hello .csv fichiers toohello conteneur par défaut sur le compte de stockage hello se trouvent sur ce [page](machine-learning-data-science-process-hive-walkthrough.md#upload).

## <a name="submit"></a>Comment les requêtes Hive toosubmit
Pour envoyer des requêtes Hive, utilisez au choix :

1. [Envoyer des requêtes Hive avec la ligne de commande Hadoop dans le nœud principal du cluster Hadoop](#headnode)
2. [Envoyer des requêtes Hive avec hello éditeur Hive](#hive-editor)
3. [Envoyer des requêtes Hive avec les commandes Azure PowerShell](#ps)

Des requêtes Hive sont similaires à SQL. Si vous êtes familiarisé avec SQL, vous souhaiterez peut-être hello [Hive pour SQL utilisateurs Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) utile.

Lorsque vous soumettez une requête Hive, vous pouvez également contrôler la destination hello de sortie de hello de requêtes Hive, qu’il s’agisse de hello écran ou tooa fichier local sur le nœud principal de hello ou tooan d’objets blob Azure.

### <a name="headnode"></a> 1. Envoyer des requêtes Hive avec la ligne de commande Hadoop dans le nœud principal du cluster Hadoop
Si la ruche hello requête est complexe, envoi que directement dans le nœud principal de hello du cluster Hadoop de hello entraîne généralement toofaster de bouclage à envoyer avec un éditeur Hive ou scripts Azure PowerShell.

Connectez-vous à toohello le nœud principal du cluster Hadoop de hello, ouvrez hello de ligne de commande Hadoop sur bureau hello de nœud principal de hello et entrez la commande `cd %hive_home%\bin`.

Vous avez des requêtes Hive de trois façons toosubmit Bonjour de ligne de commande Hadoop :

* directement ;
* à l’aide de fichiers HQL ;
* avec hello Hive console de commande

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Envoyer directement des requêtes Hive dans la ligne de commande Hadoop
Vous pouvez exécuter la commande comme `hive -e "<your hive query>;` toosubmit les requêtes Hive simples directement dans Hadoop ligne de commande. Voici un exemple, où les contours de zone hello rouge hello commande qui soumet la requête Hive de hello et hello zone verte contours hello sortie à partir de la requête de Hive hello.

![Create workspace](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>Envoyer des requêtes Hive dans des fichiers HQL
Lors de la requête de Hive hello est plus complexe et comporte plusieurs lignes, la modification de requêtes dans la ligne de commande ou de la console de commande ruche n’est pas pratique. Une alternative est toouse un éditeur de texte dans le nœud principal de hello de requêtes Hive hello Hadoop cluster toosave hello dans un fichier .hql dans un répertoire local du nœud principal de hello. Puis hello ruche requête hello .hql fichier peut être envoyée à l’aide de hello `-f` argument comme suit :

    hive -f "<path toohello .hql file>"

![Create workspace](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**Supprimer l’affichage de l’état d’avancement des requêtes Hive**

Par défaut, une fois la requête Hive est soumise en ligne de commande Hadoop, progression hello de tâche de mappage/réduction hello est imprimée sur écran. toosuppress hello impression écran de progression de la tâche hello mappage/réduction, vous pouvez utiliser un argument `-S` (« S » en majuscules) Bonjour ligne de commande comme suit :

    hive -S -f "<path toohello .hql file>"
.    hive -S -e "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>Envoyer des requêtes Hive dans la console de commande Hive
Vous pouvez également tout d’abord entrer la console de commande hello ruche en exécutant la commande `hive` de ligne de commande Hadoop, puis à soumettre les requêtes Hive dans la console de commande Hive. Voici un exemple. Dans cet exemple, hello deux zones rouges surbrillance hello commandes utilisées tooenter hello console de commande Hive et hello requête Hive soumis dans la console de commande Hive, respectivement. boîte de Hello vert met en surbrillance la sortie hello à partir de la requête de Hive hello.

![Create workspace](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

les exemples précédents Hello directement les résultats de la requête Hive hello sur l’écran de sortie. Vous pouvez également écrire le fichier local tooa sortie hello sur le nœud principal de hello ou tooan d’objets blob Azure. Ensuite, vous pouvez utiliser d’autres outils toofurther analyser la sortie hello de requêtes Hive.

**Sortie ruche requête résultats tooa du fichier local.**
toooutput ruche requête résultats tooa répertoire local sur le nœud principal de hello, vous avez toosubmit hello ruche de requête dans la ligne de commande Hadoop de hello comme suit :

    hive -e "<hive query>" > <local path in hello head node>

Dans l’exemple suivant de hello, sortie hello de requête Hive est écrit dans un fichier `hivequeryoutput.txt` dans le répertoire `C:\apps\temp`.

![Create workspace](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**Sortie tooan de résultats de requête Hive blob Azure**

Vous pouvez également produire hello ruche requête résultats tooan des objets blob Azure, dans le conteneur par défaut de hello du cluster Hadoop de hello. requête Hive de Hello pour cela est la suivante :

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

Dans l’exemple suivant de hello, sortie hello de requête Hive est écrite répertoire d’objets blob tooa `queryoutputdir` conteneur hello par défaut du cluster Hadoop de hello. Ici, vous ne devez nom du répertoire hello tooprovide, sans le nom d’objet blob hello. Une erreur est générée si vous déclarez le nom du répertoire et celui du blob, comme dans `wasb:///queryoutputdir/queryoutput.txt`.

![Create workspace](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

Si vous ouvrez le conteneur par défaut de hello du cluster Hadoop de hello à l’aide de l’Explorateur de stockage Azure, vous pouvez voir la sortie hello de requête de Hive hello comme indiqué dans la figure suivante de hello. Vous pouvez appliquer hello filtre (mis en surbrillance en rouge) tooonly récupérer hello blob avec des lettres spécifiés dans les noms.

![Create workspace](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Envoyer des requêtes Hive avec hello éditeur Hive
Vous pouvez également utiliser hello Console de requête (éditeur Hive) en entrant une URL sous forme de hello *https://&#60 ; Nom du cluster Hadoop >.azurehdinsight.net/Home/HiveEditor* dans un navigateur web. Vous devez être connecté hello voir cette console et par conséquent, vous avez besoin de vos informations d’identification Hadoop le cluster.

### <a name="ps"></a> 3. Envoyer des requêtes Hive avec les commandes Azure PowerShell
Vous pouvez également utiliser des requêtes Hive de toosubmit PowerShell. Pour obtenir de l'aide, consultez [Envoi de tâches Hive avec PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).

## <a name="create-tables"></a>Création de la base de données et des tables Hive
requêtes Hive Hello sont partagés Bonjour [référentiel GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) et peut être téléchargé à partir de là.

Voici la requête Hive hello qui crée une table Hive.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

Voici la description de hello de champs hello dont vous avez besoin tooplug dans et d’autres configurations :

* **&#60; nom de la base de données >**: nom hello de base de données hello que vous souhaitez toocreate. Si vous souhaitez simplement la base de données par défaut toouse hello, hello requête *créer la base de données...*  peut être omis.
* **&#60; nom de la table >**: nom hello de table hello que vous souhaitez toocreate au sein de la base de données spécifiée hello. Si vous souhaitez la base de données par défaut toouse hello, table de hello peut être référencé directement par *&#60; nom de la table >* sans &#60; nom de la base de données >.
* **&#60; le séparateur de champs >**: séparateur hello qui délimite les champs de toobe de fichier de données hello téléchargé toohello ruche du tableau.
* **&#60; le séparateur de ligne >**: séparateur hello qui délimite les lignes dans le fichier de données hello.
* **&#60; l’emplacement de stockage >**: hello des données de stockage Azure localisation toosave hello des tables de la ruche. Si vous ne spécifiez pas *emplacement &#60; emplacement de stockage >*, hello de base de données et tables hello sont stockées dans *hive/entrepôt/* répertoire dans un conteneur par défaut hello de cluster de ruche hello par défaut. Si vous souhaitez d’emplacement de stockage toospecify hello, emplacement de stockage hello a toobe conteneur hello par défaut pour les tables et de la base de données hello. Cet emplacement a toobe appelé conteneur d’emplacement toohello relatif par défaut du cluster hello format hello *' wasb : / / / &#60; répertoire 1 > /'* ou *' wasb : / / / &#60; répertoire 1 > / &#60; répertoire 2 > /'*, etc.. Après l’exécution de requête de hello, répertoire hello est créés dans le conteneur par défaut de hello.
* **TBLPROPERTIES("Skip.Header.Line.Count"="1")**: si le fichier de données hello possède une ligne d’en-tête, vous avez tooadd cette propriété **à fin de hello** Hello *create table* requête. Dans le cas contraire, ligne d’en-tête hello est chargé comme une table d’enregistrement toohello. Si le fichier de données hello n’a pas d’une ligne d’en-tête, cette configuration peut être omise dans la requête de hello.

## <a name="load-data"></a>Charger les tables de données tooHive
Voici la requête Hive hello qui charge des données dans une table Hive.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; les données de chemin d’accès tooblob >**: si la table Hive de hello blob fichier toobe téléchargé toohello est dans un conteneur par défaut hello de hello cluster HDInsight Hadoop, hello *&#60; les données de chemin d’accès tooblob >* devrait être au format de hello *' wasb : / / / &#60; répertoire de ce conteneur > / &#60; le nom de fichier blob >'*. fichier d’objet blob Hello peut également être dans un conteneur supplémentaire de hello cluster HDInsight Hadoop. Dans ce cas, *&#60; les données de chemin d’accès tooblob >* devrait être au format de hello *' wasb : / / &#60; nom de conteneur > @&#60; le nom de compte de stockage >.blob.core.windows.net/ &#60; nom du fichier blob >'*.

  > [!NOTE]
  > Hello blob données toobe téléchargé tooHive table a toobe dans la valeur par défaut hello ou un conteneur supplémentaire hello du compte de stockage de cluster Hadoop de hello. Dans le cas contraire, hello *charger des données* signale que qu’il ne peut pas accéder à des données de hello Échec de la requête.
  >
  >

## <a name="partition-orc"></a>Rubriques avancées : Table partitionnée et Stocker des données Hive au format ORC
Si les données de salutation sont volumineux, le partitionnement de table de hello est bénéfique pour les requêtes qui doivent uniquement tooscan plusieurs partitions de table de hello. Il est, par exemple, les données du journal de hello toopartition raisonnable d’un site web par dates.

Dans Ajout toopartitioning ruche tables, il est également utile toostore hello ruche données hello optimisées en ligne en colonnes (ORC) format. Pour plus d'informations sur le format ORC, consultez l'article <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">L'utilisation de fichiers ORC améliore les performances lorsque Hive lit, écrit et traite des données</a>.

### <a name="partitioned-table"></a>Table partitionnée
Voici la requête Hive de hello qui crée une table partitionnée et charge les données.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

Lors de l’interrogation de tables partitionnées, il est recommandé de condition de partition tooadd hello Bonjour **début** Hello `where` clause comme cela améliore l’efficacité de hello de manière significative la recherche.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>Stocker des données Hive au format ORC
Ne peut pas directement charger des données de stockage d’objets blob dans des tables de ruche qui est stocké dans un format ORC hello. Voici les étapes hello que hello que vous avez besoin de données de tooload tootake à partir d’Azure BLOB tables tooHive stockées au format ORC.

Créer une table externe **stocké le fichier en tant que texte** et charger des données à partir de la table de toohello de stockage blob.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

Créer une table interne avec hello même schéma que la table externe de hello à l’étape 1, hello le séparateur de champs et stocker hello ruche des données au format ORC hello.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

Sélectionnez les données à partir de la table externe de hello à l’étape 1 et l’insérer dans la table ORC hello

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> Si table de fichier texte hello *&#60; nom de la base de données >. &#60; nom de la table externe fichier texte >* a des partitions, à l’étape 3, hello `SELECT * FROM <database name>.<external textfile table name>` commande sélectionne hello variable de partition comme un champ dans hello retourné de jeu de données. Il insérant hello *&#60; nom de la base de données >. &#60; nom de la table ORC >* échoue depuis *&#60; nom de la base de données >. &#60; nom de la table ORC >* n’a pas de variable de partition hello comme un champ de schéma de la table hello. Dans ce cas, vous devez toospecifically hello sélectionnez champs toobe inséré trop*&#60; nom de la base de données >. &#60; nom de la table ORC >* comme suit :
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

Il est sécurisé toodrop hello *&#60; nom de la table externe fichier texte >* lorsque à l’aide de hello suivant la requête une fois les données a été insérée dans *&#60; nom de la base de données >. &#60; nom de la table ORC >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

Une fois cette procédure, vous devez disposer d’une table avec des données dans hello ORC format prêt toouse.  
