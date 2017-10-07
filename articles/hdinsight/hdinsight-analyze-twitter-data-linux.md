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
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a>Analyser des données Twitter avec Hive et Hadoop sur HDInsight

Découvrez comment toouse tooprocess Apache Hive Twitter données. résultat de Hello est une liste d’utilisateurs Twitter envoyé hello la plupart des tweets qui contiennent un mot.

> [!IMPORTANT]
> étapes de Hello dans ce document ont été testées sur HDInsight 3.6.
>
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="get-hello-data"></a>Obtenir des données de hello

Twitter vous permet de tooretrieve hello [les données de chaque tweet](https://dev.twitter.com/docs/platform-objects/tweets) sous forme de document JavaScript Objet Notation (JSON) via une API REST. [OAuth](http://oauth.net) est requis pour l’authentification toohello API.

### <a name="create-a-twitter-application"></a>Création d'une application Twitter

1. À partir d’un navigateur web, connectez-vous trop[https://apps.twitter.com/](https://apps.twitter.com/). Cliquez sur hello **Inscrivez-vous dès maintenant** lien si vous n’avez pas un compte Twitter.

2. Cliquez sur **Create New App**.

3. Renseignez les champs **Name**, **Description** et **Website**. Vous pouvez apporter une URL pour hello **site Web** champ. Hello tableau suivant illustre certaines toouse de valeurs d’exemple :

   | Champ | Valeur |
   |:--- |:--- |
   | Nom |MyHDInsightApp |
   | Description |MyHDInsightApp |
   | Website |http://www.myhdinsightapp.com |

4. Cochez la case **Yes, I agree**, puis cliquez **Create your Twitter application**.

5. Cliquez sur hello **autorisations** d’autorisations par défaut onglet hello sont **en lecture seule**.

6. Cliquez sur hello **clés et les jetons d’accès** onglet.

7. Cliquez sur **Create my access token**.

8. Cliquez sur **Test OAuth** dans hello haut à droite de la page de hello.

9. Renseignez les valeurs **consumer key**, **Consumer secret**, **Access token** et **Access token secret**.

### <a name="download-tweets"></a>Téléchargement de tweets

Hello suivant code Python télécharge 10 000 tweet Twitter et enregistrer les fichiers tooa nommé **tweets.txt**.

> [!NOTE]
> Hello suit est effectuée sur le cluster HDInsight de hello, puisque Python est déjà installé.

1. Connecter le cluster HDInsight de toohello à l’aide de SSH :

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Suivant de hello utilisez commandes tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)et d’autres packages requis :

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

4. Toocreate de commande suivant de hello d’utiliser un fichier nommé **gettweets.py**:

   ```bash
   nano gettweets.py
   ```

5. Hello utilisation après le texte en tant que contenu hello Hello **gettweets.py** fichier :

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
    > Remplacer du texte d’espace réservé de hello pour hello suivant d’éléments avec des informations de hello à partir de votre application twitter :
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. Utilisez **Ctrl + X**, puis **Y** fichier hello de toosave.

7. Utilisez hello suivant du fichier de commandes toorun hello et télécharger des tweets :

    ```bash
    python gettweets.py
    ```

    Un indicateur de progression s’affiche. Il vaut too100 % hello tweet est téléchargés.

   > [!NOTE]
   > Si l’opération prend beaucoup de temps pour tooadvance de barre de progression hello, vous devez modifier les rubriques des tendances de hello filtre tootrack. Lorsqu’il existe de nombreuses tweets sur la rubrique hello dans votre filtre, vous pouvez rapidement obtenir hello 10000 tweet si nécessaire.

### <a name="upload-hello-data"></a>Télécharger les données de salutation

tooupload hello tooHDInsight stockage des données, hello utilisation suivant de commandes :

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

Ces commandes stockent les données de salutation dans un emplacement accessible à tous les nœuds de cluster de hello.

## <a name="run-hello-hiveql-job"></a>Exécuter le travail de HiveQL hello

1. Utilisez hello suivant commande toocreate un fichier contenant les instructions HiveQL :

   ```bash
   nano twitter.hql
   ```

    Utilisez hello après le texte en tant que contenu hello du fichier de hello :

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

2. Appuyez sur **Ctrl + X**, puis appuyez sur **Y** fichier hello de toosave.
3. Utilisez hello suivant commande toorun hello que hiveql contenu dans le fichier de hello :

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    Cette commande s’exécute hello hello **twitter.hql** fichier. Une fois la requête de hello est terminée, vous voyez un `jdbc:hive2//localhost:10001/>` invite.

4. À partir de l’invite de commandes beeline hello, utilisez hello suivant tooverify de requête que les données ont été importées :

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    Cette requête retourne un maximum de 10 tweet contenant hello mot **Azure** dans le texte du message hello.

## <a name="next-steps"></a>Étapes suivantes

Vous avez appris comment tootransform un jeu de données JSON non structurée dans une table Hive structurée. toolearn en savoir plus sur la ruche sur HDInsight, consultez hello suivant des documents :

* [Prise en main de HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Analyse des données sur les retards de vol avec HDInsight](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
