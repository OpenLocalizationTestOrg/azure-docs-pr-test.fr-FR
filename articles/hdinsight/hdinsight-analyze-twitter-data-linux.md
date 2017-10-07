---
title: "aaaAnalyze données Twitter avec Apache Hive - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse utiliser Hive et Hadoop dans HDInsight tootransform des données brutes TWitter dans une table Hive interrogeable."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="2048a-103">Analyser des données Twitter avec Hive et Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="2048a-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="2048a-104">Découvrez comment toouse tooprocess Apache Hive Twitter données.</span><span class="sxs-lookup"><span data-stu-id="2048a-104">Learn how toouse Apache Hive tooprocess Twitter data.</span></span> <span data-ttu-id="2048a-105">résultat de Hello est une liste d’utilisateurs Twitter envoyé hello la plupart des tweets qui contiennent un mot.</span><span class="sxs-lookup"><span data-stu-id="2048a-105">hello result is a list of Twitter users who sent hello most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2048a-106">étapes de Hello dans ce document ont été testées sur HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="2048a-106">hello steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="2048a-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="2048a-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2048a-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2048a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-hello-data"></a><span data-ttu-id="2048a-109">Obtenir des données de hello</span><span class="sxs-lookup"><span data-stu-id="2048a-109">Get hello data</span></span>

<span data-ttu-id="2048a-110">Twitter vous permet de tooretrieve hello [les données de chaque tweet](https://dev.twitter.com/docs/platform-objects/tweets) sous forme de document JavaScript Objet Notation (JSON) via une API REST.</span><span class="sxs-lookup"><span data-stu-id="2048a-110">Twitter allows you tooretrieve hello [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="2048a-111">[OAuth](http://oauth.net) est requis pour l’authentification toohello API.</span><span class="sxs-lookup"><span data-stu-id="2048a-111">[OAuth](http://oauth.net) is required for authentication toohello API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="2048a-112">Création d'une application Twitter</span><span class="sxs-lookup"><span data-stu-id="2048a-112">Create a Twitter application</span></span>

1. <span data-ttu-id="2048a-113">À partir d’un navigateur web, connectez-vous trop[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="2048a-113">From a web browser, sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="2048a-114">Cliquez sur hello **Inscrivez-vous dès maintenant** lien si vous n’avez pas un compte Twitter.</span><span class="sxs-lookup"><span data-stu-id="2048a-114">Click hello **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="2048a-115">Cliquez sur **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="2048a-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="2048a-116">Renseignez les champs **Name**, **Description** et **Website**.</span><span class="sxs-lookup"><span data-stu-id="2048a-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="2048a-117">Vous pouvez apporter une URL pour hello **site Web** champ.</span><span class="sxs-lookup"><span data-stu-id="2048a-117">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="2048a-118">Hello tableau suivant illustre certaines toouse de valeurs d’exemple :</span><span class="sxs-lookup"><span data-stu-id="2048a-118">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="2048a-119">Champ</span><span class="sxs-lookup"><span data-stu-id="2048a-119">Field</span></span> | <span data-ttu-id="2048a-120">Valeur</span><span class="sxs-lookup"><span data-stu-id="2048a-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2048a-121">Nom</span><span class="sxs-lookup"><span data-stu-id="2048a-121">Name</span></span> |<span data-ttu-id="2048a-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="2048a-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="2048a-123">Description</span><span class="sxs-lookup"><span data-stu-id="2048a-123">Description</span></span> |<span data-ttu-id="2048a-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="2048a-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="2048a-125">Website</span><span class="sxs-lookup"><span data-stu-id="2048a-125">Website</span></span> |<span data-ttu-id="2048a-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="2048a-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="2048a-127">Cochez la case **Yes, I agree**, puis cliquez **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="2048a-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="2048a-128">Cliquez sur hello **autorisations** d’autorisations par défaut onglet hello sont **en lecture seule**.</span><span class="sxs-lookup"><span data-stu-id="2048a-128">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span>

6. <span data-ttu-id="2048a-129">Cliquez sur hello **clés et les jetons d’accès** onglet.</span><span class="sxs-lookup"><span data-stu-id="2048a-129">Click hello **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="2048a-130">Cliquez sur **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="2048a-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="2048a-131">Cliquez sur **Test OAuth** dans hello haut à droite de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="2048a-131">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>

9. <span data-ttu-id="2048a-132">Renseignez les valeurs **consumer key**, **Consumer secret**, **Access token** et **Access token secret**.</span><span class="sxs-lookup"><span data-stu-id="2048a-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="2048a-133">Téléchargement de tweets</span><span class="sxs-lookup"><span data-stu-id="2048a-133">Download tweets</span></span>

<span data-ttu-id="2048a-134">Hello suivant code Python télécharge 10 000 tweet Twitter et enregistrer les fichiers tooa nommé **tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="2048a-134">hello following Python code downloads 10,000 tweets from Twitter and save them tooa file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="2048a-135">Hello suit est effectuée sur le cluster HDInsight de hello, puisque Python est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="2048a-135">hello following steps are performed on hello HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="2048a-136">Connecter le cluster HDInsight de toohello à l’aide de SSH :</span><span class="sxs-lookup"><span data-stu-id="2048a-136">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2048a-137">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2048a-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="2048a-138">Suivant de hello utilisez commandes tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)et d’autres packages requis :</span><span class="sxs-lookup"><span data-stu-id="2048a-138">Use hello following commands tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. <span data-ttu-id="2048a-139">Toocreate de commande suivant de hello d’utiliser un fichier nommé **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="2048a-139">Use hello following command toocreate a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="2048a-140">Hello utilisation après le texte en tant que contenu hello Hello **gettweets.py** fichier :</span><span class="sxs-lookup"><span data-stu-id="2048a-140">Use hello following text as hello contents of hello **gettweets.py** file:</span></span>

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > <span data-ttu-id="2048a-141">Remplacer du texte d’espace réservé de hello pour hello suivant d’éléments avec des informations de hello à partir de votre application twitter :</span><span class="sxs-lookup"><span data-stu-id="2048a-141">Replace hello placeholder text for hello following items with hello information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="2048a-142">Utilisez **Ctrl + X**, puis **Y** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="2048a-142">Use **Ctrl + X**, then **Y** toosave hello file.</span></span>

7. <span data-ttu-id="2048a-143">Utilisez hello suivant du fichier de commandes toorun hello et télécharger des tweets :</span><span class="sxs-lookup"><span data-stu-id="2048a-143">Use hello following command toorun hello file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="2048a-144">Un indicateur de progression s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2048a-144">A progress indicator appears.</span></span> <span data-ttu-id="2048a-145">Il vaut too100 % hello tweet est téléchargés.</span><span class="sxs-lookup"><span data-stu-id="2048a-145">It counts up too100% as hello tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2048a-146">Si l’opération prend beaucoup de temps pour tooadvance de barre de progression hello, vous devez modifier les rubriques des tendances de hello filtre tootrack.</span><span class="sxs-lookup"><span data-stu-id="2048a-146">If it is taking a long time for hello progress bar tooadvance, you should change hello filter tootrack trending topics.</span></span> <span data-ttu-id="2048a-147">Lorsqu’il existe de nombreuses tweets sur la rubrique hello dans votre filtre, vous pouvez rapidement obtenir hello 10000 tweet si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2048a-147">When there are many tweets about hello topic in your filter, you can quickly get hello 10000 tweets needed.</span></span>

### <a name="upload-hello-data"></a><span data-ttu-id="2048a-148">Télécharger les données de salutation</span><span class="sxs-lookup"><span data-stu-id="2048a-148">Upload hello data</span></span>

<span data-ttu-id="2048a-149">tooupload hello tooHDInsight stockage des données, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="2048a-149">tooupload hello data tooHDInsight storage, use hello following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="2048a-150">Ces commandes stockent les données de salutation dans un emplacement accessible à tous les nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="2048a-150">These commands store hello data in a location that all nodes in hello cluster can access.</span></span>

## <a name="run-hello-hiveql-job"></a><span data-ttu-id="2048a-151">Exécuter le travail de HiveQL hello</span><span class="sxs-lookup"><span data-stu-id="2048a-151">Run hello HiveQL job</span></span>

1. <span data-ttu-id="2048a-152">Utilisez hello suivant commande toocreate un fichier contenant les instructions HiveQL :</span><span class="sxs-lookup"><span data-stu-id="2048a-152">Use hello following command toocreate a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="2048a-153">Utilisez hello après le texte en tant que contenu hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="2048a-153">Use hello following text as hello contents of hello file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
   DROP TABLE tweets;
   CREATE TABLE tweets
   (
       id BIGINT,
       created_at STRING,
       created_at_date STRING,
       created_at_year STRING,
       created_at_month STRING,
       created_at_day STRING,
       created_at_time STRING,
       in_reply_to_user_id_str STRING,
       text STRING,
       contributors STRING,
       retweeted STRING,
       truncated STRING,
       coordinates STRING,
       source STRING,
       retweet_count INT,
       url STRING,
       hashtags array<STRING>,
       user_mentions array<STRING>,
       first_hashtag STRING,
       first_user_mention STRING,
       screen_name STRING,
       name STRING,
       followers_count INT,
       listed_count INT,
       friends_count INT,
       lang STRING,
       user_location STRING,
       time_zone STRING,
       profile_image_url STRING,
       json_response STRING
   );
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
           when "Jan" then "01"
           when "Feb" then "02"
           when "Mar" then "03"
           when "Apr" then "04"
           when "May" then "05"
           when "Jun" then "06"
           when "Jul" then "07"
           when "Aug" then "08"
           when "Sep" then "09"
           when "Oct" then "10"
           when "Nov" then "11"
           when "Dec" then "12" end,
       substr (get_json_object(json_response, '$.created_at'),9,2),
       substr (get_json_object(json_response, '$.created_at'),12,8),
       get_json_object(json_response, '$.in_reply_to_user_id_str'),
       get_json_object(json_response, '$.text'),
       get_json_object(json_response, '$.contributors'),
       get_json_object(json_response, '$.retweeted'),
       get_json_object(json_response, '$.truncated'),
       get_json_object(json_response, '$.coordinates'),
       get_json_object(json_response, '$.source'),
       cast (get_json_object(json_response, '$.retweet_count') as INT),
       get_json_object(json_response, '$.entities.display_url'),
       array(
           trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
       array(
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
       trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
       trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
       get_json_object(json_response, '$.user.screen_name'),
       get_json_object(json_response, '$.user.name'),
       cast (get_json_object(json_response, '$.user.followers_count') as INT),
       cast (get_json_object(json_response, '$.user.listed_count') as INT),
       cast (get_json_object(json_response, '$.user.friends_count') as INT),
       get_json_object(json_response, '$.user.lang'),
       get_json_object(json_response, '$.user.location'),
       get_json_object(json_response, '$.user.time_zone'),
       get_json_object(json_response, '$.user.profile_image_url'),
       json_response
   WHERE (length(json_response) > 500);
   ```

2. <span data-ttu-id="2048a-154">Appuyez sur **Ctrl + X**, puis appuyez sur **Y** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="2048a-154">Press **Ctrl + X**, then press **Y** toosave hello file.</span></span>
3. <span data-ttu-id="2048a-155">Utilisez hello suivant commande toorun hello que hiveql contenu dans le fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="2048a-155">Use hello following command toorun hello HiveQL contained in hello file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="2048a-156">Cette commande s’exécute hello hello **twitter.hql** fichier.</span><span class="sxs-lookup"><span data-stu-id="2048a-156">This command runs hello hello **twitter.hql** file.</span></span> <span data-ttu-id="2048a-157">Une fois la requête de hello est terminée, vous voyez un `jdbc:hive2//localhost:10001/>` invite.</span><span class="sxs-lookup"><span data-stu-id="2048a-157">Once hello query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="2048a-158">À partir de l’invite de commandes beeline hello, utilisez hello suivant tooverify de requête que les données ont été importées :</span><span class="sxs-lookup"><span data-stu-id="2048a-158">From hello beeline prompt, use hello following query tooverify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="2048a-159">Cette requête retourne un maximum de 10 tweet contenant hello mot **Azure** dans le texte du message hello.</span><span class="sxs-lookup"><span data-stu-id="2048a-159">This query returns a maximum of 10 tweets that contain hello word **Azure** in hello message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2048a-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2048a-160">Next steps</span></span>

<span data-ttu-id="2048a-161">Vous avez appris comment tootransform un jeu de données JSON non structurée dans une table Hive structurée.</span><span class="sxs-lookup"><span data-stu-id="2048a-161">You have learned how tootransform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="2048a-162">toolearn en savoir plus sur la ruche sur HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="2048a-162">toolearn more about Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="2048a-163">Prise en main de HDInsight</span><span class="sxs-lookup"><span data-stu-id="2048a-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="2048a-164">Analyse des données sur les retards de vol avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="2048a-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
