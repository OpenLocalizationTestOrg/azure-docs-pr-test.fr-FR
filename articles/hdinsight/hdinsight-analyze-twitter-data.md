---
title: "aaaAnalyze données Twitter avec Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse ruche tooanalyze Twitter données sur Hadoop dans HDInsight toofind hello fréquence d’utilisation d’un mot particulier."
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
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>Analyse des données Twitter avec Hive dans HDInsight
Sites Web sociaux sont une des forces positives de hello principaux pour l’adoption des données volumineuses. Les API publiques fournies par des sites comme Twitter représentent une source de données utile pour l'analyse et la compréhension des tendances populaires.
Dans ce didacticiel, vous obtenir tweets à l’aide d’un API de diffusion en continu de Twitter et utilisez Apache Hive Azure HDInsight tooget une liste d’utilisateurs Twitter qui a envoyé hello la plupart des tweets contenant un mot.

> [!IMPORTANT]
> Hello étapes décrites dans ce document nécessitent un cluster HDInsight de basés sur Windows. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Pour étapes tooa spécifiques basés sur Linux de cluster, consultez [analyser Twitter des données à l’aide de la ruche dans HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello :

* **poste de travail** sur lequel Azure PowerShell est installé et configuré.

    tooexecute scripts Windows PowerShell, vous devez exécuter Azure PowerShell en tant qu’administrateur et définir la stratégie d’exécution de hello trop*RemoteSigned*. Consultez la page [Exécution de scripts Windows PowerShell][powershell-script].

    Avant d’exécuter des scripts Windows PowerShell, vérifiez que vous êtes connecté tooyour abonnement Azure à l’aide de hello suivant l’applet de commande :

    ```powershell
    Login-AzureRmAccount
    ```

    Si vous avez plusieurs abonnements Azure, utilisez hello suivant l’applet de commande tooset hello abonnement :

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017. étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.
    >
    > Suivez les étapes de hello dans [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello dernière version d’Azure PowerShell. Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.

* Un **cluster Azure HDInsight**. Pour obtenir des instructions sur l’approvisionnement des clusters, consultez la rubrique [Prise en main de HDInsight][hdinsight-get-started] ou [Approvisionnement de clusters HDInsight][hdinsight-provision]. Vous devrez le nom du cluster hello plus loin dans le didacticiel de hello.

Hello tableau suivant répertorie les fichiers hello utilisés dans ce didacticiel :

| Fichiers | Description |
| --- | --- |
| /tutorials/twitter/data/tweets.txt |données de sources Hello pour le travail de ruche hello. |
| /tutorials/twitter/output |dossier de sortie Hello pour le travail de ruche hello. Bonjour nom de fichier de sortie par défaut ruche de travail est **000000_0**. |
| tutorials/twitter/twitter.hql |fichier de script HiveQL Hello. |
| /tutorials/twitter/jobstatus |état du travail Hadoop de Hello. |

## <a name="get-twitter-feed"></a>Obtention du flux Twitter
Dans ce didacticiel, vous allez utiliser hello [Twitter API de diffusion][twitter-streaming-api]. Bonjour Twitter spécifique, vous allez utiliser des API de diffusion en continu est [États/filtre][twitter-statuses-filter].

> [!NOTE]
> Un fichier contenant 10 000 tweets et le fichier de script Hive hello (présenté dans la section suivante de hello) a été téléchargé dans un conteneur d’objets Blob public. Vous pouvez ignorer cette section si vous souhaitez que les fichiers toouse hello téléchargé.

[Données de tweets](https://dev.twitter.com/docs/platform-objects/tweets) est stocké au format JavaScript Objet Notation (JSON) hello qui contient une structure imbriquée complexe. Au lieu d’écrire de nombreuses lignes de code à l’aide d’un langage de programmation classique, vous pouvez transformer cette structure imbriquée en une table Hive, de sorte qu’un langage de type SQL, appelé HiveQL, puisse effectuer une requête sur celle-ci.

Twitter utilise l’API de tooits accès OAuth tooprovide autorisé. OAuth est un protocole d’authentification qui permet aux utilisateurs tooapprove applications tooact en leur nom sans partage son mot de passe. Plus d’informations, consultez [oauth.net](http://oauth.net/) ou Bonjour excellent [tooOAuth du Guide du débutant](http://hueniverse.com/oauth/) à partir de Hueniverse.

Hello première étape toouse OAuth est toocreate une nouvelle application sur site de développeur de Twitter hello.

**toocreate une application Twitter**

1. Connectez-vous trop[https://apps.twitter.com/](https://apps.twitter.com/). Cliquez sur hello **s’inscrire maintenant** lien si vous n’avez pas un compte Twitter.
2. Cliquez sur **Create New App**.
3. Renseignez les champs **Name**, **Description** et **Website**. Vous pouvez apporter une URL pour hello **site Web** champ. Hello tableau suivant illustre certaines toouse de valeurs d’exemple :

   | Champ | Valeur |
   | --- | --- |
   |  Nom |MyHDInsightApp |
   |  Description |MyHDInsightApp |
   |  Website |http://www.myhdinsightapp.com |
4. Cochez la case **Yes, I agree**, puis cliquez **Create your Twitter application**.
5. Cliquez sur hello **autorisations** d’autorisations par défaut onglet hello sont **en lecture seule**. Ces étapes sont suffisantes pour ce didacticiel.
6. Cliquez sur hello **clés et les jetons d’accès** onglet.
7. Cliquez sur **Create my access token**.
8. Cliquez sur **Test OAuth** dans hello haut à droite de la page de hello.
9. Renseignez les valeurs **consumer key**, **Consumer secret**, **Access token** et **Access token secret**. Vous avez besoin des valeurs de hello plus loin dans le didacticiel de hello.

Dans ce didacticiel, vous utiliserez un appel de service web de Windows PowerShell toomake hello. Pour obtenir un exemple .NET en C#, consultez la rubrique [Analyse des sentiments Twitter en temps réel avec HBase dans HDInsight][hdinsight-hbase-twitter-sentiment]. Bonjour autres appels de service web toomake outil populaire est [ *Curl*][curl]. Vous pouvez le télécharger [ici][curl-download].

> [!NOTE]
> Lorsque vous utilisez la commande de curl hello dans Windows, utilisez des guillemets doubles au lieu des guillemets simples pour les valeurs d’option hello.

**tooget tweets**

1. Ouvrez hello Windows PowerShell Integrated Scripting Environment (ISE). (Sur l’écran d’accueil de Windows 8 hello, tapez **PowerShell_ISE** puis cliquez sur **Windows PowerShell ISE**. Consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start].)
2. Copiez hello script suivant dans le volet de script hello :

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
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

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Définir des variables de tooeight de cinq premières hello dans le script de hello :

    Variable|Description
    ---|---
    $clusterName|Il s’agit de nom hello du cluster HDInsight de hello où vous souhaitez application hello de toorun.
    $oauth_consumer_key|Il s’agit d’application de Twitter hello **clé de consommateur** vous avez notées précédemment lorsque vous avez créé l’application de Twitter hello.
    $oauth_consumer_secret|Il s’agit d’application de Twitter hello **secret de consommateur** vous avez notées précédemment.
    $oauth_token|Il s’agit d’application de Twitter hello **jeton d’accès** vous avez notées précédemment.
    $oauth_token_secret|Il s’agit d’application de Twitter hello **secret du jeton d’accès** vous avez notées précédemment.
    $destBlobName|Il s’agit de nom d’objet blob de sortie de hello. la valeur par défaut Hello est **tutorials/twitter/data/tweets.txt**. Si vous modifiez la valeur par défaut de hello, vous devez les scripts Windows PowerShell tooupdate hello en conséquence.
    $trackString|service web de Hello retournera les mots clés de tweets toothese connexes. la valeur par défaut Hello est **HDInsight de Azure, le Cloud,**. Si vous modifiez la valeur par défaut de hello, vous mettrez à jour les scripts Windows PowerShell hello en conséquence.
    $lineMax|valeur de Hello détermine combien script de hello tweet lira. Il prend environ trois minutes tooread 100 Tweet. Vous pouvez définir un plus grand nombre, mais prend plus toodownload de temps.

1. Appuyez sur **F5** script de hello toorun. Si vous rencontrez des problèmes, comme une solution de contournement, sélectionnez toutes les lignes de hello, puis appuyez sur **F8**.
2. Le message « Complete! à la fin de hello de sortie de hello. S’il y a un message d’erreur, il s’affiche en rouge.

En tant qu’une procédure de validation, vous pouvez vérifier le fichier de sortie hello, **/tutorials/twitter/data/tweets.txt**, sur votre stockage d’objets Blob Azure en utilisant un Explorateur de stockage Azure ou l’Azure PowerShell. Pour obtenir un exemple de script Windows PowerShell pour répertorier les fichiers, consultez la rubrique [Utilisation de Stockage Blob avec HDInsight][hdinsight-storage-powershell].

## <a name="create-hiveql-script"></a>Créer un script HiveQL
À l’aide d’Azure PowerShell, vous pouvez exécuter plusieurs instructions HiveQL une à une heure ou package hello HiveQL instruction dans un fichier de script. Dans ce didacticiel, vous allez créer un script HiveQL. fichier de script Hello doit être téléchargé tooAzure stockage d’objets Blob. Dans la section suivante de hello, vous allez exécuter le fichier de script hello à l’aide d’Azure PowerShell.

> [!NOTE]
> fichier de script Hive Hello et un fichier contenant les 10 000 tweet ont été téléchargés dans un conteneur d’objets Blob public. Vous pouvez ignorer cette section si vous souhaitez que les fichiers toouse hello téléchargé.

Hello script HiveQL effectuera suivant de hello :

1. **Supprimer la table de tweets_raw hello** au cas où la table hello existe déjà.
2. **Créer la table de Hive hello tweets_raw**. Cette table structurée ruche temporaire conserve des données de hello pour extraire davantage, transformer et charger de traitement (ETL). Pour plus d’informations sur les partitions, consultez la rubrique [Didacticiel Hive][apache-hive-tutorial].
3. **Charger des données** à partir du dossier source hello, /tutorials/twitter/data. Hello tweet grand jeu de données au format JSON imbriquée a maintenant été transformé en une structure de table temporaire Hive.
4. **DROP hello tweet table** au cas où la table hello existe déjà.
5. **Créer hello tweet table**. Vous pouvez interroger sur hello tweet jeu de données à l’aide de ruche, vous devez toorun un autre processus ETL. Ce processus ETL définit un schéma de table plus détaillé pour les données hello que vous avez stocké dans la table « twitter_raw » de hello.
6. **Insertion de la table overwrite**. Ce script Hive complex lancera hors tension d’un ensemble de longs travaux MapReduce par cluster Hadoop de hello. Selon la taille de votre jeu de données et hello de votre cluster, ceci peut prendre environ 10 minutes.
7. **Insertion du répertoire overwrite**. Exécuter un fichier de requêtes et de sortie hello dataset tooa. Cette requête retourne une liste d’utilisateurs Twitter qui a envoyé la plupart des tweets hello mot « Azure ».

**toocreate une ruche de script et le télécharger tooAzure**

1. Ouvrez Windows PowerShell ISE.
2. Copiez hello script suivant dans le volet de script hello :

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

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Définissez tout d’abord deux variables de hello dans le script de hello :

   | Variable | Description |
   | --- | --- |
   |  $clusterName |Entrez le nom du cluster HDInsight hello où application hello de toorun. |
   |  $subscriptionID |Entrez l’identifiant de votre abonnement Azure. |
   |  $sourceDataPath |emplacement de stockage d’objets Blob Azure où les requêtes Hive hello lit hello de données à partir de Hello. Vous n’avez pas besoin toochange cette variable. |
   |  $outputPath |emplacement de stockage d’objets Blob Azure où les requêtes Hive hello produira des résultats de hello de Hello. Vous n’avez pas besoin toochange cette variable. |
   |  $hqlScriptFile |emplacement de Hello et le nom de fichier de hello hello HiveQL du fichier de script. Vous n’avez pas besoin toochange cette variable. |
4. Appuyez sur **F5** script de hello toorun. Si vous rencontrez des problèmes, comme une solution de contournement, sélectionnez toutes les lignes de hello, puis appuyez sur **F8**.
5. Le message « Complete! à la fin de hello de sortie de hello. S’il y a un message d’erreur, il s’affiche en rouge.

En tant qu’une procédure de validation, vous pouvez vérifier le fichier de sortie hello, **/tutorials/twitter/twitter.hql**, sur votre stockage d’objets Blob Azure en utilisant un Explorateur de stockage Azure ou l’Azure PowerShell. Pour obtenir un exemple de script Windows PowerShell pour répertorier les fichiers, consultez la rubrique [Utilisation de Stockage Blob avec HDInsight][hdinsight-storage-powershell].

## <a name="process-twitter-data-by-using-hive"></a>Traitement des données Twitter à l’aide de Hive
Vous avez terminé tous les travaux de préparation hello. Maintenant, vous pouvez appeler hello ruche script et vérifier les résultats de hello.

### <a name="submit-a-hive-job"></a>Soumettre un travail Hive
Utilisez hello Windows PowerShell script toorun hello ruche du script suivant. Vous devrez la première variable de tooset hello.

> [!NOTE]
> toouse hello tweet et hello script HiveQL que vous avez téléchargé dans les deux dernières sections hello, jeu $hqlScriptFile too"/tutorials/twitter/twitter.hql ». toouse hello ceux qui ont été téléchargés tooa des blob publics pour vous, définissez les $hqlScriptFile trop »wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql».

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
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

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>Vérifier les résultats de hello
Utilisez hello suivant hello toocheck de script Windows PowerShell sortie des tâches Hive. Vous devez tout d’abord deux variables de tooset hello.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
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
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> table de Hive Hello utilise \001 hello séparateur de champs. délimiteur de Hello n’est pas visible dans la sortie de hello.

Une fois les résultats de l’analyse hello ont été placés dans le stockage d’objets Blob Azure, vous pouvez exporter hello données tooan SQL Azure de base de données/SQL server, exportez hello données tooExcel à l’aide de Power Query ou connecter vos données d’application toohello à l’aide de hello Hive le pilote ODBC. Pour plus d’informations, consultez [Sqoop d’utilisation avec HDInsight][hdinsight-use-sqoop], [analyser des données de retard de vol avec HDInsight][hdinsight-analyze-flight-delay-data], [ Connecter Excel tooHDInsight avec Power Query][hdinsight-power-query], et [tooHDInsight Excel de se connecter avec Microsoft ODBC Driver de la ruche de hello][hdinsight-hive-odbc].

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, nous avons vu comment tootransform un jeu de données JSON non structurée dans un tooquery table Hive structuré, Explorer et analyser les données de Twitter à l’aide de HDInsight sur Azure. toolearn, voir :

* [Prise en main de HDInsight][hdinsight-get-started]
* [Analyse de sentiments Twitter en temps réel avec HBase dans HDInsight][hdinsight-hbase-twitter-sentiment]
* [Analyse des données sur les retards de vol avec HDInsight][hdinsight-analyze-flight-delay-data]
* [Connecter Excel tooHDInsight avec Power Query][hdinsight-power-query]
* [Rejoignez Excel tooHDInsight hello Microsoft ODBC Driver de la ruche][hdinsight-hive-odbc]
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
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
