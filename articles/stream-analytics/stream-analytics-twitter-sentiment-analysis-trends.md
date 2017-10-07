---
title: "analyse des sentiments Twitter aaaReal-temps avec Analytique de flux de données Azure | Documents Microsoft"
description: "Découvrez comment toouse Analytique de flux de données pour l’analyse de sentiments Twitter en temps réel. Obtenir des instructions à partir de toodata de génération d’événements dans un tableau de bord en direct."
keywords: "analyse de tendances twitter en temps réel, analyse de sentiments, analyse des réseaux sociaux, exemple d’analyse de tendances"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>Analyse de sentiments Twitter en temps réel dans Azure Stream Analytics

Découvrez comment toobuild analytique sociaux en mettant en temps réel dans une solution d’analyse de l’opinion Twitter événements aux concentrateurs d’événements Azure. Vous pouvez ensuite écrire les données de salutation tooanalyze une requête Analytique de flux de données Azure et un magasin hello résultats pour une utilisation ultérieure, ou utilisent un tableau de bord et [Power BI](https://powerbi.com/) insights tooprovide en temps réel.

Les outils d’analyse des réseaux sociaux aident les organisations à comprendre les tendances. Les sujets populaires sont les sujets significatifs et avis apparaissant dans un grand nombre de billets sur les réseaux sociaux. Analyse des sentiments, également appelé *mining d’avis*, utilise des attitudes sociaux analytique outils toodetermine vers un produit, l’idée et ainsi de suite. 

Analyse des tendances en temps réel Twitter est un bon exemple d’un outil analytique, comme modèle de hello #sqlhelp abonnement vous permet de toolisten (hashtags) de mots clés toospecific et développer l’analyse des sentiments Hello de flux.

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>Scénario : analyse de sentiments sur les réseaux sociaux en temps réel

Une société qui a un site Web de médias est intéressée de gagner un avantage sur ses concurrents en présentant du contenu de site est immédiatement pertinente tooits lecteurs. société de Hello utilise une analyse sociaux sur des sujets qui sont pertinentes tooreaders en effectuant une analyse des sentiments en temps réel des données de Twitter.

rubriques de tendances tooidentify en temps réel sur Twitter, hello entreprise besoins d’analytique en temps réel sur le volume de tweet de hello et opinion vis-à-vis des principales rubriques. En d’autres termes, hello est un moteur d’analytique sentiment analysis qui repose sur ce flux de médias sociaux.

## <a name="prerequisites"></a>Composants requis
Dans ce didacticiel, vous utilisez une application cliente qui se connecte tooTwitter, recherche tweet ayant certaines hashtags (que vous pouvez définir). Dans l’ordre toorun hello application et analyser hello tweet à l’aide d’Analytique de diffusion en continu d’Azure, vous devez disposer de hello :

* Un abonnement Azure
* un compte Twitter ; 
* Une application Twitter et hello [jeton d’accès OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) pour cette application. Nous fournirons des informations détaillées sur la manière de toocreate une application Twitter plus tard.
* flux d’application TwitterWPFClient Hello, qui lit hello Twitter. tooget cette application, le téléchargement hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) à partir de GitHub et puis décompressez le package de hello dans un dossier sur votre ordinateur. Si vous souhaitez toosee hello source code et exécuter l’application hello dans un débogueur, vous pouvez obtenir le code source hello de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>Créer un concentrateur Event Hub pour l’entrée Stream Analytics

exemple d’application Hello génère des événements et les transmet un concentrateur d’événements Azure tooan. Concentrateurs d’événements Azure constituent la méthode hello préféré ingestion d’événements pour l’Analytique des flux de données. Pour plus d’informations, consultez hello [documentation d’Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).


### <a name="create-an-event-hub-namespace-and-event-hub"></a>Créer un espace de noms Event Hub et un concentrateur Event Hub
Dans cette procédure, vous créez un espace de noms de concentrateur d’événements, et puis vous ajoutez un espace de noms événement hub toothat. Espaces de noms de concentrateur événement toologically groupe relatives des instances de bus d’événements. 

1. Connectez-vous à toohello portail Azure, puis cliquez sur **nouveau** > **Internet of Things** > **concentrateur d’événements**. 

2. Bonjour **créer l’espace de noms** panneau, entrez un nom d’espace de noms tels que `<yourname>-socialtwitter-eh-ns`. Vous pouvez utiliser n’importe quel nom pour l’espace de noms hello, mais le nom de hello doit être valide pour une URL et il doit être unique dans Azure. 
    
3. Sélectionnez un abonnement, créez ou choisissez un groupe de ressources, puis cliquez sur **Créer**. 

    ![Créer un espace de noms Event Hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. Lors de l’espace de noms hello a terminé le déploiement, trouver hello événement hub espace de noms dans votre liste de ressources Azure. 

5. Cliquez sur le nouvel espace de noms hello et dans le panneau espace de noms de hello, cliquez sur  **+ &nbsp;concentrateur d’événements**. 

    ![bouton de concentrateur d’événements ajouter Hello pour la création d’un concentrateur d’événements ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. Hub d’événements de nom hello `socialtwitter-eh`. Vous pouvez utiliser un autre nom. Si vous le faites, prenez note de celui-ci, car vous devez les nom hello plus tard. Vous n’avez pas besoin tooset d’autres options pour le concentrateur d’événements hello.

    ![Panneau de création d’un concentrateur Event Hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. Cliquez sur **Créer**.


### <a name="grant-access-toohello-event-hub"></a>Concentrateur d’événements grant access toohello

Avant d’un processus peut envoyer le concentrateur d’événements de données tooan, concentrateur d’événements hello doit avoir une stratégie qui autorise l’accès approprié. stratégie d’accès Hello génère une chaîne de connexion qui inclut les informations d’autorisation.

1.  Dans le panneau d’espace de noms des événements du hello, cliquez sur **concentrateurs d’événements** puis cliquez sur nom hello de votre hub d’événements.

2.  Dans le panneau de concentrateur d’événements de hello, cliquez sur **les stratégies d’accès partagé** puis cliquez sur  **+ &nbsp;ajouter**.

    >[!NOTE]
    >Assurez-vous que vous travaillez avec un concentrateur d’événements hello, pas hello événement hub espace de noms.

3.  Ajoutez la stratégie nommée `socialtwitter-access` et, pour **Revendication**, sélectionnez **Gérer**.

    ![Panneau de création d’une stratégie d’accès au concentrateur Event Hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  Cliquez sur **Créer**.

5.  Après le déploiement de stratégie de hello, sélectionnez-la dans la liste hello des stratégies d’accès partagé.

6.  Case de hello rechercher **la clé primaire de la chaîne de connexion** et cliquez sur la chaîne de connexion toohello suivant hello copie bouton. 
    
    ![Copie la clé de chaîne de connexion principale hello à partir de la stratégie d’accès hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  Collez la chaîne de connexion hello dans un éditeur de texte. Vous devez cette chaîne de connexion pour la section suivante de hello, après avoir apporté quelques tooit de petites modifications.

    chaîne de connexion Hello ressemble à ceci :

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    Notez que chaîne de connexion hello contient plusieurs paires clé-valeur, séparées par des points-virgules : `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, et `EntityPath`.  

    > [!NOTE]
    > Pour la sécurité, les parties de la chaîne de connexion hello dans hello exemple ont été supprimés.

8.  Dans l’éditeur de texte hello, supprimez hello `EntityPath` paire de chaîne de connexion hello (n’oubliez pas point-virgule hello tooremove qui le précède). Lorsque vous avez terminé, la chaîne de connexion hello ressemble à ceci :

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>Configurer et démarrer l’application cliente de Twitter hello
application cliente de Hello Obtient les événements tweet directement à partir de Twitter. Dans la commande toodo, il doit hello de toocall autorisation Twitter les API de diffusion en continu. tooconfigure que l’autorisation, que vous créez une application dans Twitter, ce qui génère des informations d’identification uniques (par exemple, un jeton OAuth). Vous pouvez ensuite configurer de hello client application toouse ces informations d’identification lorsqu’il émet des appels d’API. 

### <a name="create-a-twitter-application"></a>Création d'une application Twitter
Si vous ne possédez pas encore une application Twitter que vous pouvez utiliser pour ce didacticiel, vous pouvez en créer une. Vous devez déjà posséder un compte Twitter.

> [!NOTE]
> processus exact de Hello dans Twitter pour la création d’une application et l’obtention de jeton, des secrets et des clés de hello peut changer. Si ces instructions ne correspondent pas ce que vous voyez sur le site de Twitter hello, consultez la documentation du développeur toohello Twitter.

1. Accédez toohello [page de gestion des applications Twitter](https://apps.twitter.com/). 

2. Créez une application. 

    * Pour l’URL du site Web de hello, spécifiez une URL valide. Il n’a pas toobe un site en direct. (Vous ne pouvez pas spécifier simplement `localhost`.)
    * Renseignez le champ de rappel hello. application cliente de Hello que vous utilisez pour ce didacticiel ne requiert pas rappels.

    ![Création d’une application dans Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. Si vous le souhaitez, modifier les autorisations de l’application hello tooread uniquement.

4. Lors de l’application hello est créée, accédez à toohello **clés et les jetons d’accès** page.

5. Cliquez sur hello bouton toogenerate un jeton d’accès et le secret du jeton d’accès.

Gardez les informations utiles, car vous en aurez besoin dans la procédure suivante de hello.

>[!NOTE]
>clés de Hello et les secrets pour l’application de Twitter hello fournissent l’accès tooyour Twitter compte. Considérer ces informations comme sensibles, même hello comme vous le faites votre mot de passe Twitter. Par exemple, ne pas incorporer ces informations dans une application que vous donnez à tooothers. 


### <a name="configure-hello-client-application"></a>Configurer l’application cliente de hello
Nous avons créé une application cliente qui se connecte à l’aide des données tooTwitter [API de diffusion en continu de Twitter](https://dev.twitter.com/streaming/overview) toocollect les événements tweet sur un ensemble spécifique de rubriques. application Hello utilise hello [Sentiment140](http://help.sentiment140.com/) outil open source, qui assigne hello suivant tweet de sentiment valeur tooeach :

* 0 = négatif
* 2 = neutre
* 4 = positif

Une fois que les événements tweet hello ont été attribuées à une valeur d’indice de sentiment, elles sont appliquées concentrateur d’événements toohello que vous avez créé précédemment.

Avant l’exécution de l’application hello, il requiert certaines informations vous concernant, telles que les clés de Twitter hello et chaîne de connexion de concentrateur événement hello. Vous pouvez fournir des informations de configuration hello des façons suivantes :

* Exécutez l’application hello, puis utilisez l’application hello à tooenter hello clés, les secrets et chaîne de connexion pour l’interface utilisateur. Si vous le faites, les informations de configuration hello sont utilisées pour la session en cours, mais il n’est pas enregistré.
* Modifier le fichier .config de l’application hello et définir des valeurs hello il. Cette approche conserve les informations de configuration hello, mais il signifie également que ces informations potentiellement sensibles sont stockées en texte brut sur votre ordinateur.

Hello procédure suivante décrit les deux approches. 

1. Assurez-vous que vous avez téléchargé et décompressé hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, comme indiqué dans les conditions préalables de hello.

2. les valeurs de hello tooset en cours d’exécution (et uniquement pour hello session en cours), exécutez hello `TwitterWPFClient.exe` application. Lors de l’application hello vous y invite, entrez hello valeurs suivantes :

    * Hello Twitter consommateur clé (API).
    * Hello Twitter question secrète du client (clé secrète API).
    * Hello jeton d’accès Twitter.
    * Hello Secret du jeton accès Twitter.
    * informations de chaîne de connexion Hello que vous avez enregistré précédemment. Assurez-vous que vous utilisez de chaîne de connexion hello que vous avez supprimé hello `EntityPath` paire clé-valeur à partir de.
    * Bonjour mots clés Twitter sentiment toodetermine pour souhaitées.

   ![Application TwitterWpfClient en cours d’exécution, affichant des paramètres masqués](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. les valeurs hello tooset utilisent de manière permanente, un fichier de texte éditeur tooopen hello TwitterWpfClient.exe.config. Ensuite, dans hello `<appSettings>` élément, cela :

    * Définissez `oauth_consumer_key` toohello Twitter consommateur clé (API). 
    * Définissez `oauth_consumer_secret` toohello Twitter question secrète du client (clé secrète API).
    * Définissez `oauth_token` toohello jeton d’accès Twitter.
    * Définissez `oauth_token_secret` toohello Secret du jeton accès Twitter.

    Plus loin dans hello `<appSettings>` élément, apporter ces modifications :

    * Définissez `EventHubName` nom de hub d’événements toohello (autrement dit, toohello de valeur du chemin d’accès de hello entité).
    * Définissez `EventHubNameConnectionString` chaîne de connexion toohello. Assurez-vous que vous utilisez de chaîne de connexion hello que vous avez supprimé hello `EntityPath` paire clé-valeur à partir de.

    Hello `<appSettings>` section ressemble à hello l’exemple suivant. (Pour des raisons de clarté et de sécurité, nous avons inséré des retours automatiques de ligne et supprimé des caractères.)

    ![Fichier de configuration d’application TwitterWpfClient dans un éditeur de texte, affichant les clés de Twitter hello et des secrets et des informations de chaîne de connexion hello événement hub](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. Si vous n’avez pas déjà commencé application hello, exécutez TwitterWpfClient.exe maintenant. 

5. Cliquez sur le sentiment social du toocollect bouton vert Démarrer hello. Vous voyez les événements Tweet avec hello **créédans**, **rubrique**, et **SentimentScore** valeurs envoyées tooyour concentrateur d’événements.

    ![Application TwitterWpfClient en cours d’exécution, affichant une liste de tweets](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >Si vous constatez des erreurs, et vous ne voyez pas un flux de données de tweets affiché dans la partie inférieure de hello de fenêtre hello, vérifiez attentivement les secrets et des clés de hello. Vérifiez également la chaîne de connexion hello (Assurez-vous qu’il ne comprend pas hello `EntityPath` clé et valeur.)


## <a name="create-a-stream-analytics-job"></a>Création d’un travail Stream Analytics

Maintenant que les événements tweet sont diffusion en continu en temps réel à partir de Twitter, vous pouvez configurer un tooanalyze de tâche de flux de données Analytique ces événements en temps réel.

1. Bonjour portail Azure, cliquez sur **nouveau** > **Internet of Things** > **tâche de flux de données Analytique**.

2. Nom du travail hello `socialtwitter-sa-job` et spécifiez un abonnement, le groupe de ressources et l’emplacement.

    Il s’agit d’une bonne idée tooplace hello hello et travail de concentrateur d’événements Bonjour même région pour meilleures performances et que vous ne payez tootransfer données entre les régions.

    ![Création d’un travail Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. Cliquez sur **Créer**.

    Hello travail est créé et le portail de hello affiche les détails de la tâche.


## <a name="specify-hello-job-input"></a>Spécifier une entrée de tâche hello

1. Dans votre tâche de flux de données Analytique, sous **travail topologie** milieu hello du Panneau de tâche hello, cliquez sur **entrées**. 

2. Bonjour **entrées** panneau, cliquez sur  **+ &nbsp;ajouter** puis remplissez panneau hello avec ces valeurs :

    * **Alias d’entrée**: utiliser le nom hello `TwitterStream`. Si vous utilisez un autre nom, prenez-en note, car vous en aurez besoin ultérieurement.
    * **Type de source** : sélectionnez **Flux de données**.
    * **Source** : sélectionnez **Event Hub**.
    * **Option d’importation** : sélectionnez **Utiliser le hub d’événements de l’abonnement actuel**. 
    * **Espace de noms service bus**: sélectionnez hello événement hub namespace que vous avez créé précédemment (`<yourname>-socialtwitter-eh-ns`).
    * **Concentrateur d’événements**: concentrateur d’événements hello Select que vous avez créé précédemment (`socialtwitter-eh`).
    * **Nom de la stratégie hub événement**: sélectionnez la stratégie d’accès hello que vous avez créé précédemment (`socialtwitter-access`).

    ![Créer une entrée pour le travail Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. Cliquez sur **Créer**.


## <a name="specify-hello-job-query"></a>Spécifiez la requête de travail hello

Stream Analytics prend en charge un modèle de requête simple et déclaratif pour la description des transformations. toolearn en savoir plus sur le langage de hello, consultez hello [référence du langage de requête Azure Stream Analytique](https://msdn.microsoft.com/library/azure/dn834998.aspx).  Ce didacticiel aborde la création et le test de plusieurs requêtes sur des données Twitter.

nombre de hello toocompare de mentionne les rubriques, vous pouvez utiliser un [fenêtre bascule](https://msdn.microsoft.com/library/azure/dn835055.aspx) nombre de hello tooget de mentionne par rubrique toutes les cinq secondes.

1. Fermer hello **entrées** panneau si vous n’avez pas encore.

2. Dans le panneau de tâche hello, cliquez sur hello **requête** boîte. Azure répertorie les entrées hello et sorties qui sont configurés pour la tâche de hello et vous permet de créer une requête qui vous permet de transforment les flux d’entrée hello lors de leur envoi toohello sortie.

3. Vérifiez que hello TwitterWpfClient application est en cours d’exécution. 

3. Bonjour **requête** panneau, cliquez sur toohello suivant de points hello `TwitterStream` d’entrée, puis sélectionnez **les exemples de données à partir de l’entrée**.

    ![Menu options toouse exemples de données pour hello Analytique de diffusion en continu de la tâche entrée, « Exemples de données à partir de l’entrée « sélectionné](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    Cette opération ouvre un panneau qui vous permet de spécifier la quantité tooget de données d’exemple, définie en termes de la durée pendant laquelle le flux d’entrée tooread hello.

4. Définissez **Minutes** too3 puis cliquez sur **OK**. 
    
    ![Options d’échantillonnage de flux d’entrée de hello, avec « 3 minutes » sélectionnées.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    Azure échantillonne les données du flux d’entrée de hello sur 3 minutes et vous avertit lorsque les données d’exemple hello sont prêtes. (Cette opération prend quelques instants.) 

    Hello exemples de données sont stockées temporairement et sont disponibles tant que fenêtre de requête hello ouvert. Si vous fermez la fenêtre de requête hello, les données d’exemple hello sont ignorées, et vous avez toocreate un nouvel ensemble d’exemples de données. 

5. Modifier la requête hello dans hello code éditeur toohello suivant :

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    Si n’avez pas utilisé `TwitterStream` en tant que de hello alias pour l’entrée de hello, remplacez votre alias pour `TwitterStream` dans la requête de hello.  

    Cette requête utilise hello **TIMESTAMP BY** mot clé toospecify un champ d’horodatage dans toobe de charge utile hello utilisée dans le calcul de temporelle hello. Si ce champ n’est pas spécifié, l’opération de fenêtrage hello est effectuée à l’aide de temps hello chaque événement reçus sur le concentrateur d’événements hello. En savoir plus dans la section hello « heure d’arrivée et heure de l’Application » de [référence de flux de requête Analytique](https://msdn.microsoft.com/library/azure/dn834998.aspx).

    Cette requête accède également à un horodatage de fin hello de chaque fenêtre à l’aide de hello **System.Timestamp** propriété.

5. Cliquez sur **Test**. requête de Hello s’exécute sur des données hello vous échantillonnées.
    
6. Cliquez sur **Enregistrer**. Cela permet d’économiser les requête hello en tant que partie du travail de diffusion en continu d’Analytique hello. (Il n’enregistre pas les données d’exemple hello).


## <a name="experiment-using-different-fields-from-hello-stream"></a>Expérience à l’aide des différents champs à partir de flux de hello 

Hello tableau suivant répertorie les champs hello qui font partie de hello diffusion en continu des données JSON. Vous pouvez tooexperiment libre dans l’éditeur de requête hello.

|Propriété JSON | Définition|
|--- | ---|
|CreatedAt | temps de Hello que tweet hello a été créé.|
|Rubrique | rubrique Hello qui correspond à hello spécifié (mot clé)|
|SentimentScore | score d’opinion Hello de Sentiment140|
|Auteur | handle de Twitter Hello qui a envoyé les tweet hello|
|Texte | corps Hello de tweet de hello|


## <a name="create-an-output-sink"></a>Créer un récepteur de sortie

Vous avez ainsi défini un flux d’événements, un tooingest d’entrée de concentrateur d’événements et une requête de tooperform une transformation sur les flux hello. dernière étape de Hello est toodefine récepteur de sortie pour le travail de hello.  

Dans ce didacticiel, vous écrivez hello agrégée tweet événements à partir de hello tâche requête tooAzure stockage d’objets Blob.  Vous pouvez également transmettre des votre tooAzure de résultats de la base de données SQL, stockage de Table Azure, les concentrateurs d’événements, ou Power BI, en fonction de votre application a besoin.

## <a name="specify-hello-job-output"></a>Spécifiez la sortie des tâches hello

1. Bonjour **travail topologie** , cliquez sur hello **sortie** boîte. 

2. Bonjour **sorties** panneau, cliquez sur  **+ &nbsp;ajouter** puis remplissez panneau hello avec ces valeurs :

    * **Alias de sortie**: utiliser le nom hello `TwitterStream-Output`. 
    * **Sink** : sélectionnez **Stockage d’objets blob**.
    * **Options d’importation** : sélectionnez **Utiliser l’objet blob de stockage de l’abonnement actuel**.
    * **Compte de stockage** : sélectionnez **Créer un compte de stockage**.
    * **Compte de stockage** (seconde zone) : entrez `YOURNAMEsa`, où `YOURNAME` représente votre nom ou une autre chaîne unique. nom de Hello peut utiliser que des lettres minuscules et des chiffres, et il doit être unique dans Azure. 
    * **Conteneur** : Entrez `socialtwitter`.
    nom de compte de stockage Hello et le nom de conteneur sont tooprovide ensemble utilisé un URI pour le stockage d’objets blob hello, comme suit : 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Panneau Nouvelle sortie pour le travail Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. Cliquez sur **Créer**. 

    Azure crée le compte de stockage hello et génère une clé automatiquement. 

5. Fermer hello **sorties** panneau. 


## <a name="start-hello-job"></a>Démarrer le travail de hello

Une entrée de travail, une requête et une sortie sont spécifiées. Vous êtes la tâche de flux de données Analytique hello toostart prêt.

1. Vérifiez que hello TwitterWpfClient application est en cours d’exécution. 

2. Dans le panneau de tâche hello, cliquez sur **Démarrer**.

    ![Démarrer la tâche de flux de données Analytique hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. Bonjour **Start job** panneau, pour **heure de début de sortie des tâches**, sélectionnez **maintenant** puis cliquez sur **Démarrer**. 

    ![Panneau de « Démarrer le travail » pour la tâche de flux de données Analytique hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure vous avertit de hello le travail a démarré, et dans le panneau de tâche hello, hello état affiché est **en cours d’exécution**.

    ![Travail en cours d’exécution](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>Afficher la sortie de l’analyse de sentiments

Une fois votre travail a démarré en cours d’exécution et traite les flux Twitter en temps réel hello, vous pouvez afficher la sortie hello pour l’analyse de sentiments.

Vous pouvez utiliser un outil tel que [Azure Storage Explorer](https://http://storageexplorer.com/) ou [Explorateur Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview votre tâche de sortie en temps réel. À ce stade, vous pouvez utiliser [Power BI](https://powerbi.com/) tooextend votre tooinclude application un tableau de bord personnalisé comme hello celui affiché dans hello suivant capture d’écran :

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>Créer une autre requête tooidentify les rubriques des tendances

Une autre requête, vous pouvez utiliser toounderstand Twitter sentiment est basée sur un [fenêtre glissante](https://msdn.microsoft.com/library/azure/dn835051.aspx). rubriques de tendances tooidentify, vous recherchez les rubriques qui dépassent un seuil pour mentionne dans un laps de temps.

Pour des raisons de hello de ce didacticiel, vous recherchez les rubriques mentionnées plus de 20 fois Bonjour dernière 5 secondes.

1. Dans le panneau de tâche hello, cliquez sur **arrêter** tâche hello de toostop. 

2. Bonjour **travail topologie** , cliquez sur hello **requête** boîte. 

3. Modifier les paramètres toohello hello requête suivants :

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. Cliquez sur **Enregistrer**.

5. Vérifiez que hello TwitterWpfClient application est en cours d’exécution. 

6. Cliquez sur **Démarrer** tâche hello de toorestart à l’aide de la nouvelle requête de hello.


## <a name="get-support"></a>Obtenir de l'aide
Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
