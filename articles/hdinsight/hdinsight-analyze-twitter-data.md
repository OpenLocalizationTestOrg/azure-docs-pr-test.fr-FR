---
title: "Analyse des données Twitter avec Hadoop dans HDInsight - Azure | Microsoft Docs"
description: "Découvrez comment utiliser Hive pour analyser des données Twitter sur Hadoop dans HDInsight afin de déterminer la fréquence d'utilisation d'un mot particulier."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a5f97dfa084291cefde9bf27b5639926de1bc80e
ms.sourcegitcommit: f8437edf5de144b40aed00af5c52a20e35d10ba1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>Analyse des données Twitter avec Hive dans HDInsight
Les sites web sociaux constituent l’un des principaux motifs de l’utilisation du modèle « Big Data ». Les API publiques fournies par des sites comme Twitter représentent une source de données utile pour l'analyse et la compréhension des tendances populaires.
Dans ce didacticiel, vous allez recevoir des tweets à l’aide de l’API de diffusion Twitter, puis utiliser Apache Hive sur Azure HDInsight pour récupérer une liste des utilisateurs de Twitter ayant envoyé le plus de tweets contenant un mot donné.

> [!IMPORTANT]
> Les étapes décrites dans ce document nécessitent un cluster HDInsight Windows. Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Pour les étapes spécifiques à un cluster basé sur Linux, consultez la rubrique [Analyse des données Twitter avec Hive dans HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :

* **poste de travail** sur lequel Azure PowerShell est installé et configuré.

    Pour exécuter des scripts Windows PowerShell, vous devez exécuter Azure PowerShell en tant qu’administrateur et définir la stratégie d’exécution sur *RemoteSigned*. Consultez la page [Exécution de scripts Windows PowerShell][powershell-script].

    Avant d’exécuter vos scripts Windows PowerShell, assurez-vous que vous êtes connecté à votre abonnement Azure à l’aide de l’applet de commande suivante :

    ```powershell
    Login-AzureRmAccount
    ```

    Si vous possédez plusieurs abonnements Azure, utilisez l’applet de commande suivante pour définir l'abonnement en cours :

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017. Dans ce document, la procédure repose sur les nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.
    >
    > Suivez les étapes indiquées dans [Installation et de configuration d’Azure PowerShell](/powershell/azureps-cmdlets-docs) pour installer la dernière version d’Azure PowerShell. Si vous devez modifier certains scripts pour utiliser les nouvelles applets de commande fonctionnant avec Azure Resource Manager, consultez [Migration vers les outils de développement Azure Resource Manager pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.

* Un **cluster Azure HDInsight**. Pour obtenir des instructions sur l’approvisionnement des clusters, consultez la rubrique [Prise en main de HDInsight][hdinsight-get-started] ou [Approvisionnement de clusters HDInsight][hdinsight-provision]. Vous en aurez besoin plus loin dans le didacticiel.

Le tableau suivant répertorie les fichiers utilisés dans ce didacticiel :

| Fichiers | Description |
| --- | --- |
| /tutorials/twitter/data/tweets.txt |Données source pour la tâche Hive. |
| /tutorials/twitter/output |Données de sortie pour la tâche Hive. Par défaut, le nom du fichier de sortie de la tâche Hive est **000000_0**. |
| tutorials/twitter/twitter.hql |Fichier de script HiveQL. |
| /tutorials/twitter/jobstatus |État de la tâche Hadoop. |

## <a name="get-twitter-feed"></a>Obtention du flux Twitter
Dans ce didacticiel, vous allez utiliser les [API de diffusion Twitter][twitter-streaming-api]. L’API de diffusion Twitter spécifique que vous allez utiliser est [statuses/filter][twitter-statuses-filter].

> [!NOTE]
> Un fichier contenant 10 000 tweets et le fichier de script Hive (traité dans la section suivante) ont été téléchargés dans un conteneur d'objets blob public. Vous pouvez ignorer cette section si vous souhaitez utiliser les fichiers téléchargés.

[données des tweets](https://dev.twitter.com/docs/platform-objects/tweets) sont stockées au format JSON (JavaScript Object Notation) qui contient une structure imbriquée complexe. Au lieu d’écrire de nombreuses lignes de code à l’aide d’un langage de programmation classique, vous pouvez transformer cette structure imbriquée en une table Hive, de sorte qu’un langage de type SQL, appelé HiveQL, puisse effectuer une requête sur celle-ci.

Twitter utilise OAuth pour fournir un accès autorisé à son API. OAuth est un protocole d’authentification qui permet aux utilisateurs d’autoriser des applications à agir à leur place sans partager leur mot de passe. Pour plus d'informations, consultez la page [oauth.net](http://oauth.net/) ou l'excellent [Guide du débutant sur OAuth](http://hueniverse.com/oauth/) de Hueniverse.

Pour utiliser OAuth, la première étape consiste à créer une nouvelle application sur le site du développeur Twitter.

**Pour créer une application Twitter**

1. Connectez-vous à [https://apps.twitter.com/](https://apps.twitter.com/). Cliquez sur le lien **Sign up now** si vous ne possédez pas de compte Twitter.
2. Cliquez sur **Create New App**.
3. Renseignez les champs **Name**, **Description** et **Website**. Vous pouvez créer une URL pour le champ **Website** . Le tableau suivant affiche quelques exemples de valeurs à utiliser :

   | Champ | Valeur |
   | --- | --- |
   |  Nom |MyHDInsightApp |
   |  Description |MyHDInsightApp |
   |  Website |http://www.myhdinsightapp.com |
4. Cochez la case **Yes, I agree**, puis cliquez **Create your Twitter application**.
5. Cliquez sur l'onglet **Permissions** . L'autorisation par défaut est **Read only**. Ces étapes sont suffisantes pour ce didacticiel.
6. Cliquez sur l’onglet **Keys and Access Tokens** .
7. Cliquez sur **Create my access token**.
8. Cliquez sur **Test OAuth** dans le coin supérieur droit de la page.
9. Renseignez les valeurs **consumer key**, **Consumer secret**, **Access token** et **Access token secret**. Vous en aurez besoin plus loin dans le didacticiel.

Dans ce didacticiel, vous allez utiliser Windows PowerShell pour effectuer l’appel du service web. L’autre outil connu permettant d’effectuer des appels de service Web est [*Curl*][curl]. Vous pouvez le télécharger [ici][curl-download].

> [!NOTE]
> Lorsque vous utilisez la commande Curl sous Windows, remplacez les guillemets simples par des guillemets doubles pour exprimer la valeur des options.

**Pour récupérer des tweets**

1. Ouvrez l’environnement d’écriture de scripts intégré de Windows PowerShell (ISE). (Sur l’écran de démarrage de Windows 8, tapez **PowerShell_ISE**, puis cliquez sur **Windows PowerShell ISE**. Consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start].)
2. Copiez le script suivant dans le volet du script :

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter the HDInsight cluster name

    # Enter the OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves the tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets the tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # The script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get the default storage account name and Blob container name using the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define the Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets to Blob storage
    Write-Host "Write to the destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Définissez les cinq premières variables du script :

    Variable|Description
    ---|---
    $clusterName|Nom du cluster HDInsight où vous souhaitez exécuter l’application.
    $oauth_consumer_key|**Clé** que vous avez notée auparavant en créant l’application Twitter.
    $oauth_consumer_secret|**Secret** que vous avez écrit auparavant pour l'application Twitter.
    $oauth_token|**Jeton d'accès** que vous avez écrit auparavant pour l'application Twitter.
    $oauth_token_secret|**Secret de jeton d'accès** que vous avez écrit auparavant pour l'application Twitter.
    $destBlobName|Nom de l'objet blob de sortie. La valeur par défaut est **tutorials/twitter/data/tweets.txt**. Si vous modifiez la valeur par défaut, vous devez mettre à jour les scripts Windows PowerShell en conséquence.
    $trackString|Le service Web renvoie les tweets liés à ces mots clés. La valeur par défaut est **Azure, Cloud, HDInsight**. Si vous modifiez la valeur par défaut, vous devez mettre à jour les scripts Windows PowerShell en conséquence.
    $lineMax|La valeur détermine le nombre de tweets lus par le script. La lecture de 100 tweets prend environ trois minutes. Vous pouvez définir un nombre plus important, mais le téléchargement prendra plus de temps.

1. Appuyez sur **F5** pour exécuter le script. Si vous êtes confronté à des problèmes, vous pouvez, pour les contourner, sélectionner toutes les lignes et appuyer ensuite sur **F8**.
2. Le message « Complete! » doit normalement s'afficher à la fin de la sortie. S’il y a un message d’erreur, il s’affiche en rouge.

Dans le cadre d’une procédure de validation, vous pouvez vérifier le fichier de sortie, **/tutorials/twitter/data/tweets.txt**, sur votre stockage d’objets blob Azure à l’aide d’un explorateur de stockage Azure ou d’Azure PowerShell. Pour obtenir un exemple de script Windows PowerShell pour répertorier les fichiers, consultez la rubrique [Utilisation de Stockage Blob avec HDInsight][hdinsight-storage-powershell].

## <a name="create-hiveql-script"></a>Créer un script HiveQL
À l'aide d'Azure PowerShell, vous pouvez exécuter plusieurs instructions HiveQL, une par une, ou empaqueter l'instruction HiveQL dans un fichier de script. Dans ce didacticiel, vous allez créer un script HiveQL. Le fichier de script doit être téléchargé dans le stockage d’objets blob Azure. Dans la section suivante, vous allez exécuter le fichier de script à l’aide d’Azure PowerShell.

> [!NOTE]
> Le fichier de script Hive et un fichier contenant 10 000 tweets ont été téléchargés dans un conteneur d'objets Blob public. Vous pouvez ignorer cette section si vous souhaitez utiliser les fichiers téléchargés.

Le script HiveQL exécutera les opérations suivantes :

1. **Suppression de la table tweets_raw** au cas où la table existe déjà.
2. **Création de la table tweets_raw Hive**. Cette table Hive structurée et temporaire conserve les données en vue d’un traitement ETL ultérieur (extraction, modification et chargement). Pour plus d’informations sur les partitions, consultez la rubrique [Didacticiel Hive][apache-hive-tutorial].
3. **Chargement des données** à partir du dossier source, /tutorials/twitter/data. Le volumineux jeu de données des tweets imbriqué dans le format JSON a été transformé en une structure de table Hive temporaire.
4. **Suppression de la table tweets** , le cas échéant.
5. **Création de la table tweets**. Avant de pouvoir effectuer une requête sur le jeu de données des tweets à l’aide de Hive, vous devez exécuter un autre processus ETL. Ce dernier définit un schéma de table plus détaillé pour les données que vous avez stockées dans la table « twitter_raw ».
6. **Insertion de la table overwrite**. Ce script Hive complexe démarre un ensemble de longues tâches MapReduce sur le cluster Hadoop. Selon votre ensemble de données et la taille de votre cluster, cela peut prendre environ 10 minutes.
7. **Insertion du répertoire overwrite**. Exécutez une requête et sortez le jeu de données dans un fichier. Cette requête renvoie une liste d’utilisateurs de Twitter dont la majorité des tweets envoyés contenaient le mot « Azure ».

**Pour créer un script Hive et le télécharger sur Azure**

1. Ouvrez Windows PowerShell ISE.
2. Copiez le script suivant dans le volet du script :

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

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

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
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

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing the Hive script file
    Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define the connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing the hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write the Hive script file to Blob storage
    Write-Host "Write to the destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Définissez les deux premières variables du script :

   | Variable | Description |
   | --- | --- |
   |  $clusterName |Entrez le nom du cluster HDInsight où vous souhaitez exécuter l'application. |
   |  $subscriptionID |Entrez l’identifiant de votre abonnement Azure. |
   |  $sourceDataPath |Emplacement de stockage d’objets blob Azure où les requêtes Hive lisent les données. Vous n'avez pas besoin de modifier cette variable. |
   |  $outputPath |Emplacement de stockage d’objets blob Azure où les requêtes Hive envoient les résultats. Vous n'avez pas besoin de modifier cette variable. |
   |  $hqlScriptFile |Emplacement et nom du fichier de script HiveQL. Vous n'avez pas besoin de modifier cette variable. |
4. Appuyez sur **F5** pour exécuter le script. Si vous êtes confronté à des problèmes, vous pouvez, pour les contourner, sélectionner toutes les lignes et appuyer ensuite sur **F8**.
5. Le message « Complete! » doit normalement s'afficher à la fin de la sortie. S’il y a un message d’erreur, il s’affiche en rouge.

Dans le cadre d’une procédure de validation, vous pouvez vérifier le fichier de sortie, **/tutorials/twitter/twitter.hql**, sur votre stockage d’objets blob Azure à l’aide d’un explorateur de stockage Azure ou d’Azure PowerShell. Pour obtenir un exemple de script Windows PowerShell pour répertorier les fichiers, consultez la rubrique [Utilisation de Stockage Blob avec HDInsight][hdinsight-storage-powershell].

## <a name="process-twitter-data-by-using-hive"></a>Traitement des données Twitter à l’aide de Hive
Vous avez terminé tout le travail de préparation. Vous pouvez à présent appeler le script Hive et vérifier les résultats.

### <a name="submit-a-hive-job"></a>Soumettre un travail Hive
Utilisez le script Windows PowerShell suivant pour exécuter le script Hive. Vous devez définir la première variable.

> [!NOTE]
> Pour utiliser les tweets et le script HiveQL que vous avez téléchargé dans les deux dernières sections, définissez la valeur $hqlScriptFile sur "/ tutorials/twitter/twitter.hql". Pour utiliser ceux qui ont été chargés sur un objet blob public pour vous, définissez $hqlScriptFile sur « wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql ».

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of the following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create the HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display the standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-the-results"></a>Vérification des résultats
Exécutez le script Windows PowerShell suivant pour vérifier la sortie de la tâche Hive. Vous devez définir les deux premières variables.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # The name of the blob to be downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download the blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display the output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> La table Hive utilise \001 comme délimiteur de champ. Le délimiteur n'est pas visible dans la sortie.

Une fois que les résultats d’analyse ont été placés dans le stockage d’objets blob Azure, vous pouvez exporter les données dans la base de données Azure SQL/le serveur SQL, exporter les données dans Excel à l’aide de Power Query ou connecter votre application aux données à l’aide du pilote ODBC Hive. Pour plus d’informations, consultez les rubriques [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop], [Analyse des données sur les retards de vol avec HDInsight][hdinsight-analyze-flight-delay-data], [Connexion d’Excel à HDInsight à l’aide de Power Query][hdinsight-power-query] et [Connexion d’Excel à HDInsight à l’aide du pilote ODBC Microsoft Hive][hdinsight-hive-odbc].

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, nous avons vu comment transformer le jeu de données JSON non structuré en une table Hive structurée pour effectuer une requête sur les données, les explorer et les analyser à partir de Twitter à l’aide de HDInsight sur Azure. Pour plus d'informations, consultez les rubriques suivantes :

* [Prise en main de HDInsight][hdinsight-get-started]
* [Analyse des données sur les retards de vol avec HDInsight][hdinsight-analyze-flight-delay-data]
* [Connexion d’Excel à HDInsight à l’aide de Power Query][hdinsight-power-query]
* [Connexion d’Excel à HDInsight à l’aide du pilote ODBC Microsoft Hive][hdinsight-hive-odbc]
* [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]:hadoop/apache-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]:hadoop/hdinsight-use-sqoop.md
[hdinsight-power-query]:hadoop/apache-hadoop-connect-excel-power-query.md
[hdinsight-hive-odbc]:hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md
