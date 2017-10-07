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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="58e7c-103">Génération de recommandations de films à l’aide d’Apache Mahout avec Hadoop sous Linux dans HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="58e7c-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="58e7c-104">Découvrez comment toouse hello [Apache Mahout](http://mahout.apache.org) bibliothèque d’apprentissage machine avec les recommandations de films toogenerate Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58e7c-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span>

<span data-ttu-id="58e7c-105">Mahout est une bibliothèque [Machine Learning][ml] pour Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="58e7c-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="58e7c-106">Mahout contient des algorithmes pour le traitement des données, tel que le filtrage, la classification et le clustering.</span><span class="sxs-lookup"><span data-stu-id="58e7c-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="58e7c-107">Dans cet article, vous utilisez une recommandation moteur toogenerate film recommandations basées sur les films vos amis se sont affiché.</span><span class="sxs-lookup"><span data-stu-id="58e7c-107">In this article, you use a recommendation engine toogenerate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58e7c-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="58e7c-108">Prerequisites</span></span>

* <span data-ttu-id="58e7c-109">Un cluster HDInsight sous Linux</span><span class="sxs-lookup"><span data-stu-id="58e7c-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="58e7c-110">Pour plus d’informations sur la création de ce dernier, consultez [Prise en main de Hadoop sous Linux dans HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="58e7c-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58e7c-111">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="58e7c-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="58e7c-112">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="58e7c-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="58e7c-113">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="58e7c-113">An SSH client.</span></span> <span data-ttu-id="58e7c-114">Pour plus d’informations, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="58e7c-114">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="58e7c-115">Contrôle de version Mahout</span><span class="sxs-lookup"><span data-stu-id="58e7c-115">Mahout versioning</span></span>

<span data-ttu-id="58e7c-116">Pour plus d’informations sur la version de hello de Mahout dans HDInsight, consultez [HDInsight versions et composants de Hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="58e7c-116">For more information about hello version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="58e7c-117"><a name="recommendations"></a>Présentation des recommandations</span><span class="sxs-lookup"><span data-stu-id="58e7c-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="58e7c-118">Une des fonctions hello fournie par Mahout est un moteur de recommandation.</span><span class="sxs-lookup"><span data-stu-id="58e7c-118">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="58e7c-119">Ce moteur accepte les données au format hello de `userID`, `itemId`, et `prefValue` (hello préférence pour un élément de hello).</span><span class="sxs-lookup"><span data-stu-id="58e7c-119">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello preference for hello item).</span></span> <span data-ttu-id="58e7c-120">Mahout peut effectuer une occurrence de collaboration analysis toodetermine : *les utilisateurs qui ont une préférence pour un élément ont également une préférence de ces autres éléments*.</span><span class="sxs-lookup"><span data-stu-id="58e7c-120">Mahout can then perform co-occurance analysis toodetermine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="58e7c-121">Mahout détermine ensuite les utilisateurs avec les préférences de l’élément de type, qui peuvent être utilisé toomake recommandations.</span><span class="sxs-lookup"><span data-stu-id="58e7c-121">Mahout then determines users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="58e7c-122">Bonjour workflow suivant est un exemple simplifié qui utilise des données de film :</span><span class="sxs-lookup"><span data-stu-id="58e7c-122">hello following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="58e7c-123">**Occurrence coadministrateurs**: Joe, Alice et Bob connexes tous les *étoile se*, *hello avertissements Empire précédent*, et *retour Hello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="58e7c-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="58e7c-124">Mahout détermine que les utilisateurs, comme l’un de ces films également comme hello deux autres.</span><span class="sxs-lookup"><span data-stu-id="58e7c-124">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="58e7c-125">**Occurrence coadministrateurs**: Bob et Alice également aimé *hello fantôme Menace*, *attaque de Clones de hello*, et *Vengeance Hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="58e7c-125">**Co-occurance**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="58e7c-126">Mahout détermine que les utilisateurs aimé les films de trois précédente hello également, tels que ces trois films.</span><span class="sxs-lookup"><span data-stu-id="58e7c-126">Mahout determines that users who liked hello previous three movies also like these three movies.</span></span>

* <span data-ttu-id="58e7c-127">**Recommandation de similarité**: Joe car aimé hello les trois premiers films, Mahout examine les films que d’autres personnes avec des préférences similaires plaît, mais Joe n’a pas observé (aimé/nominale).</span><span class="sxs-lookup"><span data-stu-id="58e7c-127">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="58e7c-128">Dans ce cas, vous recommande de Mahout *hello fantôme Menace*, *attaque de Clones de hello*, et *Vengeance Hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="58e7c-128">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="58e7c-129">Présentation des données de salutation</span><span class="sxs-lookup"><span data-stu-id="58e7c-129">Understanding hello data</span></span>

<span data-ttu-id="58e7c-130">De façon pratique, [GroupLens Research][movielens] fournit des données d’évaluation de films dans un format compatible avec Mahout.</span><span class="sxs-lookup"><span data-stu-id="58e7c-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="58e7c-131">Ces données sont disponibles sur le stockage par défaut de votre cluster à `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="58e7c-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="58e7c-132">Il existe deux fichiers, `moviedb.txt` et `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="58e7c-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="58e7c-133">fichier de ratings.txt de l’utilisateur de Hello est utilisé lors de l’analyse, alors que moviedb.txt est plus d’informations texte convivial tooprovide utilisé lors de l’affichage des résultats d’analyse de hello hello.</span><span class="sxs-lookup"><span data-stu-id="58e7c-133">hello user-ratings.txt file is used during analysis, while moviedb.txt is used tooprovide user-friendly text information when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="58e7c-134">les données d’utilisateur-ratings.txt Hello possède une structure de `userID`, `movieID`, `userRating`, et `timestamp`, qui indique comment recommandé de chaque utilisateur avec un film.</span><span class="sxs-lookup"><span data-stu-id="58e7c-134">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="58e7c-135">Voici un exemple de données de hello :</span><span class="sxs-lookup"><span data-stu-id="58e7c-135">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a><span data-ttu-id="58e7c-136">Exécuter l’analyse de hello</span><span class="sxs-lookup"><span data-stu-id="58e7c-136">Run hello analysis</span></span>

<span data-ttu-id="58e7c-137">À partir d’un cluster de toohello connexion SSH, utilisez hello suivant le travail de commande toorun hello recommandation :</span><span class="sxs-lookup"><span data-stu-id="58e7c-137">From an SSH connection toohello cluster, use hello following command toorun hello recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="58e7c-138">travail de Hello peut prendre plusieurs minutes toocomplete et peut exécuter plusieurs tâches MapReduce.</span><span class="sxs-lookup"><span data-stu-id="58e7c-138">hello job may take several minutes toocomplete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-hello-output"></a><span data-ttu-id="58e7c-139">Vue hello sortie</span><span class="sxs-lookup"><span data-stu-id="58e7c-139">View hello output</span></span>

1. <span data-ttu-id="58e7c-140">Une fois que hello est terminée, utilisez hello après la sortie de commande tooview hello généré :</span><span class="sxs-lookup"><span data-stu-id="58e7c-140">Once hello job completes, use hello following command tooview hello generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="58e7c-141">sortie de Hello apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="58e7c-141">hello output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="58e7c-142">première colonne de Hello est hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="58e7c-142">hello first column is hello `userID`.</span></span> <span data-ttu-id="58e7c-143">Hello les valeurs contenues dans ' [' et ']' sont `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="58e7c-143">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="58e7c-144">Vous pouvez utiliser sortie hello, ainsi que de hello moviedb.txt, tooprovide plus d’informations sur les recommandations hello.</span><span class="sxs-lookup"><span data-stu-id="58e7c-144">You can use hello output, along with hello moviedb.txt, tooprovide more information on hello recommendations.</span></span> <span data-ttu-id="58e7c-145">Tout d’abord, nous devons les fichiers de hello toocopy localement à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="58e7c-145">First, we need toocopy hello files locally using hello following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="58e7c-146">Cette commande copie hello fichier de tooa de données de sortie nommé **recommendations.txt** hello répertoire en cours, ainsi que les fichiers de données de film hello.</span><span class="sxs-lookup"><span data-stu-id="58e7c-146">This command copies hello output data tooa file named **recommendations.txt** in hello current directory, along with hello movie data files.</span></span>

3. <span data-ttu-id="58e7c-147">Utilisez hello suivant commande toocreate un script Python qui recherche les noms de film pour les données de hello dans la sortie de recommandations hello :</span><span class="sxs-lookup"><span data-stu-id="58e7c-147">Use hello following command toocreate a Python script that looks up movie names for hello data in hello recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="58e7c-148">Lorsque l’éditeur hello s’ouvre, utilisez hello après le texte en tant que contenu hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="58e7c-148">When hello editor opens, use hello following text as hello contents of hello file:</span></span>

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

    <span data-ttu-id="58e7c-149">Appuyez sur **Ctrl-X**, **Y**et enfin **entrée** toosave les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="58e7c-149">Press **Ctrl-X**, **Y**, and finally **Enter** toosave hello data.</span></span>

4. <span data-ttu-id="58e7c-150">Exécutez le script de Python hello.</span><span class="sxs-lookup"><span data-stu-id="58e7c-150">Run hello Python script.</span></span> <span data-ttu-id="58e7c-151">Hello commande suivante suppose que vous êtes dans le répertoire hello où tous les fichiers de hello ont été téléchargés :</span><span class="sxs-lookup"><span data-stu-id="58e7c-151">hello following command assumes you are in hello directory where all hello files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="58e7c-152">Cette commande examine les recommandations hello générées pour 4 de l’ID d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58e7c-152">This command looks at hello recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="58e7c-153">Hello **utilisateur-ratings.txt** fichier est utilisé tooretrieve films qui ont été évalués.</span><span class="sxs-lookup"><span data-stu-id="58e7c-153">hello **user-ratings.txt** file is used tooretrieve movies that have been rated.</span></span>

    * <span data-ttu-id="58e7c-154">Hello **moviedb.txt** fichier est utilisé tooretrieve les noms de hello de films de hello.</span><span class="sxs-lookup"><span data-stu-id="58e7c-154">hello **moviedb.txt** file is used tooretrieve hello names of hello movies.</span></span>

    * <span data-ttu-id="58e7c-155">Hello **recommendations.txt** est utilisé tooretrieve recommandations de films hello pour cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58e7c-155">hello **recommendations.txt** is used tooretrieve hello movie recommendations for this user.</span></span>

     <span data-ttu-id="58e7c-156">la sortie de cette commande est similaire toohello suivant texte Hello :</span><span class="sxs-lookup"><span data-stu-id="58e7c-156">hello output from this command is similar toohello following text:</span></span>

        <span data-ttu-id="58e7c-157">Un score de sept ans dans Tibet (1997) = 5.0 Indiana Jones et hello dernière Crusade (1989), un score de = 5.0 Jaws (1975), le score = 5.0 sens et la sensibilité (1995), le score = 5.0 l’indépendance (ID4) (1996), score = 5.0 mon meilleur ami mariage (1997), le score = 5.0 Jerry Maguire (1996 ), score = 5.0 Scream 2 (1997), score = 5.0 temps tooKill, (1996), score = 5.0</span><span class="sxs-lookup"><span data-stu-id="58e7c-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and hello Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time tooKill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="58e7c-158">Suppression des données temporaires</span><span class="sxs-lookup"><span data-stu-id="58e7c-158">Delete temporary data</span></span>

<span data-ttu-id="58e7c-159">Mahout travaux ne supprimez pas les données temporaires qui sont créées lors du traitement du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="58e7c-159">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="58e7c-160">Hello `--tempDir` est précisé dans hello exemple travail tooisolate hello des fichiers temporaires dans un chemin d’accès spécifique pour la suppression simple.</span><span class="sxs-lookup"><span data-stu-id="58e7c-160">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="58e7c-161">fichiers temporaires de tooremove hello, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="58e7c-161">tooremove hello temp files, use hello following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="58e7c-162">Si vous souhaitez commande hello de toorun à nouveau, vous devez également supprimer répertoire de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="58e7c-162">If you want toorun hello command again, you must also delete hello output directory.</span></span> <span data-ttu-id="58e7c-163">Utilisez hello suivant toodelete ce répertoire :</span><span class="sxs-lookup"><span data-stu-id="58e7c-163">Use hello following toodelete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="58e7c-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58e7c-164">Next steps</span></span>

<span data-ttu-id="58e7c-165">Maintenant que vous avez appris comment toouse Mahout, connaître les autres méthodes de travail avec des données sur HDInsight :</span><span class="sxs-lookup"><span data-stu-id="58e7c-165">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="58e7c-166">Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e7c-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="58e7c-167">Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e7c-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="58e7c-168">MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e7c-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
