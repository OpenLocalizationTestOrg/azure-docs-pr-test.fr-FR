---
title: "fonctionnalités aaaCreate pour les données dans un cluster Hadoop à l’aide de requêtes Hive | Documents Microsoft"
description: "Exemples de requêtes Hive qui génèrent des fonctionnalités dans les données stockées dans un cluster Azure HDInsight Hadoop."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Création de fonctionnalités pour les données dans un cluster Hadoop à l'aide de requêtes Hive
Ce document montre comment les fonctionnalités toocreate pour les données stockées dans un cluster Azure HDInsight Hadoop à l’aide de requêtes Hive. Ces requêtes Hive utilisent la ruche utilisateur défini par les fonctions incorporées (UDF), les scripts de hello pour lequel sont fournis.

fonctionnalités de toocreate Hello opérations nécessaires peuvent être gourmandes en mémoire. performances Hello de requêtes Hive devient plus importante dans ce cas et peuvent être améliorées en ajustant certains paramètres. Hello réglage de ces paramètres est décrite dans la section finale de hello.

Exemples de requêtes hello présentés sont spécifique toohello [NYC Taxi voyage données](http://chriswhong.com/open-data/foil_nyc_taxi/) scénarios sont également fournis dans [référentiel GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Ces requêtes déjà le schéma de données spécifié et sont prêt toobe soumis toorun. Dans la section finale de hello, les paramètres que les utilisateurs peuvent paramétrer afin que hello les performances des requêtes Hive peuvent être améliorées sont également décrites.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Cela **menu** lie tootopics qui décrivent comment toocreate pour les données dans différents environnements. Cette tâche est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez :

* Créé un compte Azure Storage. Pour des instructions, voir [Créer un compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Configurer un cluster Hadoop personnalisée avec hello service HDInsight.  Si vous avez besoin d'aide, consultez [Personnaliser des clusters Hadoop Azure HDInsight pour l'analyse avancée](machine-learning-data-science-customize-hadoop-cluster.md).
* les données de salutation a été téléchargé tooHive des tables dans les clusters Azure HDInsight Hadoop. Si ce n’est pas le cas, suivez les [créer et charger des tables de tooHive données](machine-learning-data-science-move-hive-tables.md) tooupload données tooHive tout d’abord les tables.
* Cluster de toohello activé l’accès à distance. Si vous avez besoin d’instructions, consultez [hello d’accès nœud principal de Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="hive-featureengineering"></a>Génération de fonctionnalités
Dans cette section, plusieurs exemples de méthodes hello dans lequel fonctionnalités peuvent générer à l’aide de requêtes Hive sont décrites. Une fois que vous avez généré des fonctionnalités supplémentaires, vous pouvez les ajouter en tant que table de colonnes toohello existante ou créer une table avec des fonctionnalités supplémentaires hello et une clé primaire, qui peut ensuite être joint avec la table d’origine de hello. Voici des exemples de hello présentées :

1. [Génération de fonctionnalités basées sur la fréquence](#hive-frequencyfeature)
2. [Risques de variables catégorielles en classification binaire](#hive-riskfeature)
3. [Extraction de fonctionnalités à partir de champs d’horodatage](#hive-datefeatures)
4. [Extraction de fonctionnalités à partir de champs de texte](#hive-textfeatures)
5. [Calcul de la distance entre des coordonnées GPS](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>Génération de fonctionnalités basées sur la fréquence
Il est souvent utile toocalculate les fréquences de hello de niveaux hello d’une variable catégorielle, ou des fréquences de hello de certaines combinaisons de niveaux à partir de plusieurs variables catégorielles. Les utilisateurs peuvent utiliser hello suivant script toocalculate ces fréquences :

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>Risques de variables catégorielles en classification binaire
Dans la classification binaire, nous avons besoin des variables catégorielles tooconvert non numérique en fonctionnalités numériques quand des modèles hello utilisés uniquement avoir des fonctionnalités numériques. Pour ce faire, chaque niveau non numérique est remplacé par un risque numérique. Dans cette section, nous montrent certaines requêtes Hive génériques qui calculent des valeurs de risque hello (notation d’évidence) d’une variable par catégorie.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

Dans cet exemple, les variables `smooth_param1` et `smooth_param2` sont toosmooth hello risque valeurs calculées à partir des données de hello. Les risques sont compris entre -Inf et Inf. Risques > 0 indique que probabilité hello que qui ciblent hello est égal too1 est supérieure à 0,5.

Une fois que le tableau des risques hello est calculée, les utilisateurs peuvent affecter tableau tooa des valeurs risque en établissant une jointure avec la table de risques hello. requête de jointure Hive Hello a été fourni dans la section précédente.

### <a name="hive-datefeatures"></a>Extraction de fonctionnalités à partir de champs d'horodatage
Hive est livré avec un ensemble de FDU pour traiter des champs d’horodatage. Dans la ruche, format de date/heure hello par défaut est ' AAAA-MM-JJ 00:00:00 » (« 1970-01-01 12:21:32 » par exemple). Dans cette section, nous affichons les exemples qui extraient jour hello d’un mois, le mois hello à partir d’un champ de date/heure et autres exemples qui convertissent une chaîne de date/heure dans un format autre que la chaîne de date/heure tooa hello par défaut format format par défaut.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

Cette requête Hive suppose que hello *&#60; champ datetime >* est au format de datetime hello par défaut.

Si un champ de date/heure n’est pas dans le format par défaut de hello, vous devez tout d’abord de champ de date/heure tooconvert hello dans horodatage Unix, puis convertir hello Unix heure datetime tooa de tampon de chaîne qui est par défaut de hello format. Lorsque hello datetime est par défaut de format, les utilisateurs peuvent appliquer hello incorporé datetime UDF tooextract fonctionnalités.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

Dans cette requête, si hello *&#60; champ datetime >* a chaîne hello like *26/03/2015 12:04:39*, hello *' &#60; le modèle de champ de date/heure hello >'* doit être `'MM/dd/yyyy HH:mm:ss'`. tootest, les utilisateurs peuvent exécuter

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

Hello *hivesampletable* dans cette requête est préinstallé sur tous les clusters Azure HDInsight Hadoop par défaut lors de l’approvisionnement des clusters de hello.

### <a name="hive-textfeatures"></a>Extraction de fonctionnalités à partir de champs de texte
Lors de la table de Hive hello possède un champ de texte qui contient une chaîne de mots qui sont délimitées par des espaces, hello requête suivante extrait la longueur de chaîne de hello et nombre de hello de mots dans la chaîne de hello hello.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>Calcul de la distance entre des coordonnées GPS
requête Hello fournie dans cette section peut être appliqué directement toohello NYC Taxi voyage données. Hello cette requête vise tooshow comment tooapply incorporé des fonctions mathématiques dans la ruche toogenerate fonctionnalités.

les champs qui sont utilisés dans cette requête Hello sont coordonnées GPS de hello des emplacements de collecte et cette chute, nommés *collecte\_longitude*, *collecte\_latitude*,  *Cette chute\_longitude*, et *cette chute\_latitude*. requêtes Hello qui calculent hello directe séparant les coordonnées de collecte et cette chute hello sont :

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

les équations mathématiques Hello qui calculent la distance entre deux coordonnées GPS hello se trouvent sur hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">mobile Type Scripts</a> site, créé par Peter Lapisu. Dans son Javascript, hello fonction `toRad()` est simplement *lat_or_lon*pi/180 *, qui convertit les degrés tooradians. Ici, *lat_or_lon* est hello latitude ou longitude. Étant donné que la ruche ne fournit pas de fonction hello `atan2`, mais fournit une fonction de hello `atan`, hello `atan2` fonction est implémentée par `atan` fonction Bonjour ci-dessus requête Hive à l’aide de la définition de hello fournie dans <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.

![Create workspace](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Une liste complète de la ruche UDF incorporées se trouvent dans hello **des fonctions intégrées** section hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">wiki d’Apache Hive</a>).  

## <a name="tuning"></a>Rubriques avancées : régler les paramètres de la ruche tooImprove vitesse des requêtes
Bonjour le paramètre par défaut les paramètres de la ruche du cluster ne peuvent pas être appropriées pour les requêtes Hive hello et données hello de traitement des requêtes hello. Dans cette section, nous expliquons certains paramètres que les utilisateurs peuvent paramétrer qui améliorent les performances de hello de requêtes Hive. Les utilisateurs ont besoin de paramètre de hello tooadd paramétrage des requêtes avant de requêtes hello de traitement de données.

1. **Espace du tas de Java**: pour les requêtes impliquant la jointure de grands jeux de données ou le traitement des enregistrements de type long, **espace du tas insuffisant** est une des erreurs courantes de hello. Cela peut être réglée en définissant des paramètres *mapreduce.map.java.opts* et *mapreduce.task.io.sort.mb* toodesired valeurs. Voici un exemple :
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    Ce paramètre alloue de l’espace de segment de mémoire de 4 Go de mémoire tooJava et rend également tri plus efficace en allouant plus de mémoire pour celle-ci. Il est un tooplay recommandé avec ces allocations s’il existe un espace de travail échec erreurs tooheap connexes.

1. **Taille de bloc DFS** : ce paramètre définit hello plus petite unité de données hello magasins de système de fichiers. Par exemple, si la taille de bloc hello DFS est de 128 Mo, puis toutes les données de taille too128MB et inférieur à sont stockées dans un bloc unique, lors des données qui sont supérieures à 128 Mo est alloué blocs supplémentaires. En choisissant une taille de bloc très faible entraîne la dégradation volumineuse dans Hadoop comme nœud de nom hello a tooprocess nombreux plusieurs demandes toofind hello pertinentes bloc se rapportant toohello fichier. Lorsque vos données ont une taille supérieure ou égale à plusieurs gigaoctets, la valeur suivante est recommandée :
   
        set dfs.block.size=128m;
2. **Optimisation d’opération de jointure dans la ruche** : lors des opérations de jointure dans le cadre de MapReduce hello ont généralement lieu dans hello réduire phase, parfois, payantes peuvent être obtenus en planifiant des jointures dans la phase de mappage hello (également appelé « mapjoins »). toodirect la ruche toodo cette mesure du possible, nous pouvons définir :
   
        set hive.auto.convert.join=true;
3. **Spécifiant le nombre de hello de mappeurs tooHive** : tandis que Hadoop permet hello tooset utilisateur hello de REDUCTEURS nombre, hello nombre de mappeurs est généralement ne pas être défini par l’utilisateur de hello. Une astuce qui permet un certain contrôle sur ce nombre est variables Hadoop hello toochoose *mapred.min.split.size* et *mapred.max.split.size* comme taille de hello de chaque plan de tâche est déterminé par :
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    En règle générale, hello valeur par défaut de *mapred.min.split.size* est 0, celle de *mapred.max.split.size* est **Long.MAX** et celle de *dfs.block.size* est de 64 Mo. Comme nous pouvons le voir, taille des données hello donné, ces paramètres par « configuration » de réglage les permet nous tootune hello nombre de mappeurs utilisé.
4. D’autres **options avancées** optimisant les performances de Hive sont indiquées ci-dessous. Ceux-ci vous toomap de mémoire allouée tooset hello et réduisent les tâches et peuvent être utiles pour ajuster les performances. Gardez à l’esprit que hello *mapreduce.reduce.memory.mb* ne peut pas être supérieure à la taille de mémoire physique hello de chaque nœud de travail dans un cluster Hadoop de hello.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

