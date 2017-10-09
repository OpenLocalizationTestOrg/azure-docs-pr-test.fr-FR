---
title: "aaaSample des données dans les tables de la ruche de HDInsight Azure | Documents Microsoft"
description: "Sous-échantillonnage de données dans des tables Hive Azure HDInsight (Hadoop)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Échantillonner des données dans des tables Hive Azure HDInsight
Dans cet article, nous décrivons comment toodown-exemples de données stockées dans les tables de la ruche HDInsight Azure à l’aide de requêtes Hive. Nous abordons trois méthodes d’échantillonnage communément utilisées :

* Échantillonnage aléatoire uniforme
* Échantillonnage aléatoire par groupe
* Échantillonnage stratifié

suivant de Hello **menu** lie tootopics qui décrivent comment toosample des données à partir de différents environnements de stockage.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Pourquoi échantillonner vos données ?**
Si dataset hello vous envisagez de tooanalyze est grand, il est généralement un tooreduce de données recommandé toodown-exemple hello il tooa plus petite mais représentatif et plus facile à gérer la taille. Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités. Son rôle dans hello processus de science des données équipe est tooenable le prototypage rapide des fonctions de traitement des données de hello et modèles d’apprentissage automatique.

Cette tâche d’échantillonnage est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-toosubmit-hive-queries"></a>Comment les requêtes Hive toosubmit
Requêtes Hive peuvent être envoyés à partir de la console de ligne de commande Hadoop hello sur le nœud principal de hello du cluster Hadoop de hello. toodo cela, ouvrez une session sur le nœud principal de hello du cluster Hadoop de hello, ouvrez hello console de ligne de commande Hadoop et soumettre des requêtes de ruche hello à partir de là. Pour obtenir des instructions sur la soumission de requêtes Hive dans la console de ligne de commande Hadoop hello, consultez [comment tooSubmit requêtes Hive](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a> Échantillonnage aléatoire uniforme
Échantillonnage aléatoire uniforme signifie que chaque ligne dans le jeu de données hello autant de chance d’échantillonnage. Cela peut être implémentée en ajoutant un jeu de données de champ supplémentaire rand() toohello dans la requête « select » interne de hello et dans hello la requête « select » externe cette condition sur un champ aléatoire.

Voici un exemple de requête :

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

Ici, `<sample rate, 0-1>` spécifie la proportion de hello d’enregistrements que les utilisateurs de hello souhaitent toosample.

## <a name="group"></a> Échantillonnage aléatoire par groupe
Lorsque les données catégoriques d’échantillonnage, vous pouvez tooeither inclure ou exclure toutes les instances de hello d’une valeur particulière d’une variable par catégorie. C’est ce que signifie le terme « échantillonnage par groupe ».
Par exemple, si vous avez une variable catégorique « État », qui a des valeurs NY, MA, autorité de certification, NJ, PA, etc., vous souhaitez que les enregistrements de hello même état toujours être ensemble, si elles sont échantillonnées ou non.

Voici un exemple de requête effectuant un échantillonnage par groupe :

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a>Échantillonnage stratifié
Échantillonnage aléatoire est stratifié avec égard tooa variable catégorielle lorsque des échantillons hello obtenus ont des valeurs catégorielles qui qui se trouvent dans hello même rapport, comme le remplissage de parent hello à partir de quels hello exemples ont été obtenues. À l’aide de hello même exemple que ci-dessus, supposons que vos données ont des alimentations sous-chemin par les États, par exemple NJ a 100 observations, NY a 60 observations, et WA a 300 observations. Si vous spécifiez le taux de hello de stratifié d’échantillonnage toobe 0,5, puis hello échantillon obtenu doit avoir environ 50, 30 et 150 observations NJ NY et WA respectivement.

Voici un exemple de requête :

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


Pour plus d’informations sur les méthodes d’échantillonnage plus élaborées qui sont disponibles dans Hive, consultez la page consacrée aux [méthodes d’échantillonnage dans le manuel du langage](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).

