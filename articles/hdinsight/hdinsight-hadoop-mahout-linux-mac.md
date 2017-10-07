---
title: "recommandations aaaGenerate à l’aide de Mahout et HDInsight (SSH) - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello Apache Mahout apprentissage des recommandations de films bibliothèque toogenerate avec HDInsight (Hadoop)."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>Génération de recommandations de films à l’aide d’Apache Mahout avec Hadoop sous Linux dans HDInsight (SSH)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Découvrez comment toouse hello [Apache Mahout](http://mahout.apache.org) bibliothèque d’apprentissage machine avec les recommandations de films toogenerate Azure HDInsight.

Mahout est une bibliothèque [Machine Learning][ml] pour Apache Hadoop. Mahout contient des algorithmes pour le traitement des données, tel que le filtrage, la classification et le clustering. Dans cet article, vous utilisez une recommandation moteur toogenerate film recommandations basées sur les films vos amis se sont affiché.

## <a name="prerequisites"></a>Composants requis

* Un cluster HDInsight sous Linux Pour plus d’informations sur la création de ce dernier, consultez [Prise en main de Hadoop sous Linux dans HDInsight][getstarted].

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un client SSH. Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

## <a name="mahout-versioning"></a>Contrôle de version Mahout

Pour plus d’informations sur la version de hello de Mahout dans HDInsight, consultez [HDInsight versions et composants de Hadoop](hdinsight-component-versioning.md).

## <a name="recommendations"></a>Présentation des recommandations

Une des fonctions hello fournie par Mahout est un moteur de recommandation. Ce moteur accepte les données au format hello de `userID`, `itemId`, et `prefValue` (hello préférence pour un élément de hello). Mahout peut effectuer une occurrence de collaboration analysis toodetermine : *les utilisateurs qui ont une préférence pour un élément ont également une préférence de ces autres éléments*. Mahout détermine ensuite les utilisateurs avec les préférences de l’élément de type, qui peuvent être utilisé toomake recommandations.

Bonjour workflow suivant est un exemple simplifié qui utilise des données de film :

* **Occurrence coadministrateurs**: Joe, Alice et Bob connexes tous les *étoile se*, *hello avertissements Empire précédent*, et *retour Hello Jedi*. Mahout détermine que les utilisateurs, comme l’un de ces films également comme hello deux autres.

* **Occurrence coadministrateurs**: Bob et Alice également aimé *hello fantôme Menace*, *attaque de Clones de hello*, et *Vengeance Hello Sith*. Mahout détermine que les utilisateurs aimé les films de trois précédente hello également, tels que ces trois films.

* **Recommandation de similarité**: Joe car aimé hello les trois premiers films, Mahout examine les films que d’autres personnes avec des préférences similaires plaît, mais Joe n’a pas observé (aimé/nominale). Dans ce cas, vous recommande de Mahout *hello fantôme Menace*, *attaque de Clones de hello*, et *Vengeance Hello Sith*.

### <a name="understanding-hello-data"></a>Présentation des données de salutation

De façon pratique, [GroupLens Research][movielens] fournit des données d’évaluation de films dans un format compatible avec Mahout. Ces données sont disponibles sur le stockage par défaut de votre cluster à `/HdiSamples/HdiSamples/MahoutMovieData`.

Il existe deux fichiers, `moviedb.txt` et `user-ratings.txt`. fichier de ratings.txt de l’utilisateur de Hello est utilisé lors de l’analyse, alors que moviedb.txt est plus d’informations texte convivial tooprovide utilisé lors de l’affichage des résultats d’analyse de hello hello.

les données d’utilisateur-ratings.txt Hello possède une structure de `userID`, `movieID`, `userRating`, et `timestamp`, qui indique comment recommandé de chaque utilisateur avec un film. Voici un exemple de données de hello :

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>Exécuter l’analyse de hello

À partir d’un cluster de toohello connexion SSH, utilisez hello suivant le travail de commande toorun hello recommandation :

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> travail de Hello peut prendre plusieurs minutes toocomplete et peut exécuter plusieurs tâches MapReduce.

## <a name="view-hello-output"></a>Vue hello sortie

1. Une fois que hello est terminée, utilisez hello après la sortie de commande tooview hello généré :

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    sortie de Hello apparaît comme suit :

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    première colonne de Hello est hello `userID`. Hello les valeurs contenues dans ' [' et ']' sont `movieId`:`recommendationScore`.

2. Vous pouvez utiliser sortie hello, ainsi que de hello moviedb.txt, tooprovide plus d’informations sur les recommandations hello. Tout d’abord, nous devons les fichiers de hello toocopy localement à l’aide de hello suivant de commandes :

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    Cette commande copie hello fichier de tooa de données de sortie nommé **recommendations.txt** hello répertoire en cours, ainsi que les fichiers de données de film hello.

3. Utilisez hello suivant commande toocreate un script Python qui recherche les noms de film pour les données de hello dans la sortie de recommandations hello :

    ```bash
    nano show_recommendations.py
    ```

    Lorsque l’éditeur hello s’ouvre, utilisez hello après le texte en tant que contenu hello du fichier de hello :

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    Appuyez sur **Ctrl-X**, **Y**et enfin **entrée** toosave les données de salutation.

4. Exécutez le script de Python hello. Hello commande suivante suppose que vous êtes dans le répertoire hello où tous les fichiers de hello ont été téléchargés :

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    Cette commande examine les recommandations hello générées pour 4 de l’ID d’utilisateur.

    * Hello **utilisateur-ratings.txt** fichier est utilisé tooretrieve films qui ont été évalués.

    * Hello **moviedb.txt** fichier est utilisé tooretrieve les noms de hello de films de hello.

    * Hello **recommendations.txt** est utilisé tooretrieve recommandations de films hello pour cet utilisateur.

     la sortie de cette commande est similaire toohello suivant texte Hello :

        Un score de sept ans dans Tibet (1997) = 5.0 Indiana Jones et hello dernière Crusade (1989), un score de = 5.0 Jaws (1975), le score = 5.0 sens et la sensibilité (1995), le score = 5.0 l’indépendance (ID4) (1996), score = 5.0 mon meilleur ami mariage (1997), le score = 5.0 Jerry Maguire (1996 ), score = 5.0 Scream 2 (1997), score = 5.0 temps tooKill, (1996), score = 5.0

## <a name="delete-temporary-data"></a>Suppression des données temporaires

Mahout travaux ne supprimez pas les données temporaires qui sont créées lors du traitement du travail de hello. Hello `--tempDir` est précisé dans hello exemple travail tooisolate hello des fichiers temporaires dans un chemin d’accès spécifique pour la suppression simple. fichiers temporaires de tooremove hello, utilisez hello de commande suivante :

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> Si vous souhaitez commande hello de toorun à nouveau, vous devez également supprimer répertoire de sortie hello. Utilisez hello suivant toodelete ce répertoire :
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment toouse Mahout, connaître les autres méthodes de travail avec des données sur HDInsight :

* [Hive avec HDInsight](hdinsight-use-hive.md)
* [Pig avec HDInsight](hdinsight-use-pig.md)
* [MapReduce avec HDInsight](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
