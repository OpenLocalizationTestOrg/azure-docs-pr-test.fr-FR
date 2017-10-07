# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Prise en main de l’utilisation d’Azure Stream Analytics : détection des fraudes en temps réel

Ce didacticiel fournit une illustration de bout en bout de la toouse Analytique de flux de données Azure. Vous allez apprendre à effectuer les actions suivantes : 

* Insérer des événements de flux dans une instance d’Azure Event Hubs. Dans ce didacticiel, vous allez utiliser une application que nous fournissons pour simuler un flux d’enregistrements de métadonnées de téléphone mobile.

* Écrire des données de tootransform requêtes Analytique de flux de données de type SQL, les informations d’agrégation ou de recherche des modèles. Vous verrez comment toouse un tooexamine requête hello flux entrant et recherchez les appels qui peuvent être frauduleuses.

* Envoyer hello résultats tooan récepteur de sortie (stockage) que vous pouvez analyser des informations supplémentaires. Dans ce cas, vous allez envoyer le stockage Blob tooAzure hello appel suspectes données.

Dans ce didacticiel, nous utilisons exemple hello de la détection des fraudes en temps réel en fonction des données d’appel téléphonique. Mais technique hello que nous illustrent est également adapté pour les autres types de détection des fraudes, comme l’usurpation d’identité ou de fraude carte de crédit. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>Scénario : détection des fraudes de télécommunication et SIM en temps réel

Une société de télécommunication dispose d’un volume important de données pour les appels entrants. société de Hello veut toodetect frauduleux appelle en temps réel afin qu’ils peuvent informe les clients ou l’arrêt du service pour un nombre spécifique. Un type de fraude de carte SIM implique plusieurs appels à partir de hello même identité autour hello même moment mais dans des emplacements géographiquement différentes. toodetect ce type de fraude, hello les enregistrements entrants téléphone société besoins tooexamine et rechercher des modèles spécifiques, dans ce cas, pour les appels effectués autour hello simultanément dans différents pays. Tous les enregistrements de téléphone qui appartiennent à cette catégorie sont écrites toostorage pour une analyse ultérieure.

## <a name="prerequisites"></a>Composants requis

Dans ce didacticiel, vous allez simuler des données d’appels téléphoniques à l’aide d’une application cliente générant un exemple de métadonnées d’appel téléphonique. Certains des enregistrements hello hello application produit ressemblent à des appels frauduleuses. 

Avant de commencer, assurez-vous que vous avez hello suivantes :

* Un compte Azure.
* application de générateur Hello événement d’appel. Vous pouvez l’obtenir en le téléchargeant hello [TelcoGenerator.zip fichier](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) de hello Microsoft Download Center. Décompressez ce package dans un dossier de votre ordinateur. Si vous souhaitez que le code source de hello toosee et application hello exécution dans un débogueur, vous pouvez obtenir le code source des application hello de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

    >[!NOTE]
    >Windows peut bloquer le fichier .zip de hello téléchargé. Si vous ne pouvez pas décompresser, cliquez sur le fichier de hello et sélectionnez **propriétés**. Si vous voyez hello message « ce fichier provient d’un autre ordinateur et peut être bloqué toohelp protéger cet ordinateur », sélectionnez hello **Unblock** option, puis cliquez sur **appliquer**.

Si vous souhaitez que les résultats de hello tooexamine du travail de diffusion en continu d’Analytique hello, vous devez également un outil pour afficher le contenu de hello d’un conteneur de stockage d’objets Blob Azure. Si vous utilisez Visual Studio, vous pouvez utiliser [Azure Tools pour Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) ou [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer). Vous pouvez également installer des outils autonomes comme [Explorateur de stockage Azure](http://storageexplorer.com/) ou [Explorateur Azure](http://www.cerebrata.com/products/azure-explorer/introduction). 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Créer un événement Azure événements tooingest de concentrateurs

tooanalyze un flux de données, vous *réception* dans Azure. Un moyen le plus simple de données de tooingest est toouse [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md), ce qui permet la réception des millions d’événements par seconde, puis traiter et stocker des informations sur les événements hello. Pour ce didacticiel, vous créez un hub d’événements, puis hello événement d’appel générateur application envoi appel données toothat concentrateur d’événements. Pour plus d’informations sur les concentrateurs d’événements, consultez hello [documentation d’Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus/).

>[!NOTE]
>Pour obtenir une version plus détaillée de cette procédure, consultez [créer un espace de noms de concentrateurs d’événements et un concentrateur d’événements à l’aide de hello Azure portal](../event-hubs/event-hubs-create.md). 

### <a name="create-a-namespace-and-event-hub"></a>Créer un concentrateur Event Hub et un espace de noms
Dans cette procédure, vous créez un espace de noms de concentrateur d’événements et vous ajoutez ensuite un namepsace de toothat événements hub. Espaces de noms de concentrateur événement toologically groupe relatives des instances de bus d’événements. 

1. Ouvrez une session hello portail Azure, puis cliquez sur **nouveau** > **Internet of Things** > **concentrateur d’événements**. 

2. Bonjour **créer l’espace de noms** panneau, entrez un nom d’espace de noms tels que `<yourname>-eh-ns-demo`. Vous pouvez utiliser n’importe quel nom pour l’espace de noms hello, mais le nom de hello doit être valide pour une URL et il doit être unique dans Azure. 
    
3. Sélectionnez un abonnement, créez ou choisissez un groupe de ressources, puis cliquez sur **Créer**. 

    ![Créer un espace de noms Event Hub](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. Lors de l’espace de noms hello a terminé le déploiement, trouver hello événement hub espace de noms dans votre liste de ressources Azure. 

5. Cliquez sur le nouvel espace de noms hello et dans le panneau espace de noms de hello, cliquez sur  **+ &nbsp;concentrateur d’événements**. 

    ![bouton de concentrateur d’événements ajouter Hello pour la création d’un concentrateur d’événements ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. Hub d’événements de nom hello `sa-eh-frauddetection-demo`. Vous pouvez utiliser un autre nom. Si vous le faites, prenez note de celui-ci, car vous devez les nom hello plus tard. Vous n’avez pas besoin tooset d’autres options pour le concentrateur d’événements hello dès maintenant.

    ![Panneau de création d’un concentrateur Event Hub](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. Cliquez sur **Créer**.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>Accordez le concentrateur d’événements toohello accès et obtenir une chaîne de connexion

Avant d’un processus peut envoyer le concentrateur d’événements de données tooan, concentrateur d’événements hello doit avoir une stratégie qui autorise l’accès approprié. stratégie d’accès Hello génère une chaîne de connexion qui inclut les informations d’autorisation.

1.  Dans le panneau d’espace de noms des événements du hello, cliquez sur **concentrateurs d’événements** puis cliquez sur nom hello de votre hub d’événements.

2.  Dans le panneau de concentrateur d’événements de hello, cliquez sur **les stratégies d’accès partagé** puis cliquez sur  **+ &nbsp;ajouter**.

    >[!NOTE]
    >Assurez-vous que vous travaillez avec un concentrateur d’événements hello, pas hello événement hub espace de noms.

3.  Ajoutez la stratégie nommée `sa-policy-manage-demo` et, pour **Revendication**, sélectionnez **Gérer**.

    ![Panneau de création d’une stratégie d’accès au concentrateur Event Hub](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  Cliquez sur **Créer**.

5.  Après le déploiement de stratégie de hello, sélectionnez-la dans la liste hello des stratégies d’accès partagé.

6.  Case de hello rechercher **la clé primaire de la chaîne de connexion** et cliquez sur la chaîne de connexion toohello suivant hello copie bouton. 
    
    ![Copie la clé de chaîne de connexion principale hello à partir de la stratégie d’accès hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  Collez la chaîne de connexion hello dans un éditeur de texte. Vous devez cette chaîne de connexion pour la section suivante de hello, après avoir apporté quelques tooit de petites modifications.

    chaîne de connexion Hello ressemble à ceci :

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    Notez que chaîne de connexion hello contient plusieurs paires clé-valeur, séparées par des points-virgules : `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, et `EntityPath`.  

## <a name="configure-and-start-hello-event-generator-application"></a>Configurer et démarrer l’application de générateur d’événements hello

Avant de commencer, hello TelcoGenerator application, configurez-le afin qu’il enverra un concentrateur d’événements toohello enregistrements appel que vous venez de créer.

### <a name="configure-hello-telcogeneratorapp"></a>Configurer hello TelcoGeneratorapp

1.  Dans l’éditeur de hello où vous avez copié la chaîne de connexion hello, prenez note de hello `EntityPath` valeur et supprimez hello `EntityPath` paire (n’oubliez pas point-virgule hello tooremove qui le précède). 

2.  Dans le dossier hello où vous avez décompressé les fichiers de TelcoGenerator.zip hello, ouvrez le fichier de telcodatagen.exe.config de hello dans un éditeur. (Il existe plus d’un fichier .config, assurez-vous que vous ouvrez droite hello).

3.  Bonjour `<appSettings>` élément, cela :

    * La valeur hello Hello `EventHubName` nom de hub d’événements toohello clé (autrement dit, toohello de valeur du chemin d’accès de hello entité).
    * La valeur hello Hello `Microsoft.ServiceBus.ConnectionString` la clé de chaîne de connexion toohello. 

    Hello `<appSettings>` section ressemblera à hello l’exemple suivant. (Pour plus de clarté, nous hello lignes avec et supprimer des caractères à partir du jeton d’autorisation de hello.)

    ![Fichier de configuration d’application TelcoGenerator affichant la chaîne de connexion et de nom de hub d’événement hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Enregistrez le fichier de hello. 

### <a name="start-hello-app"></a>Démarrer l’application hello
1.  Ouvrez une fenêtre de commande et modifier le dossier toohello où hello TelcoGenerator application est décompressée.
2.  Entrez hello de commande suivante :

        telcodatagen.exe 1000 .2 2

    paramètres de Hello sont : 

    * Nombre d’enregistrements des détails des appels par heure. 
    * Probabilité de fraude de carte SIM : Fréquence, en pourcentage de tous les appels, cette application hello doit simuler un appel frauduleux. valeur de Hello.2 signifie qu’environ 20 % des enregistrements d’appel hello apparaîtront frauduleuses.
    * Durée en heures. nombre de Hello d’heures hello application doit s’exécuter. Vous pouvez également arrêter application hello tout moment en appuyant sur Ctrl + C à la ligne de commande hello.

    Après quelques secondes, application hello démarre l’affichage des enregistrements de l’appel téléphonique sur l’écran hello comme il les envoie le concentrateur d’événements toohello.

Certains des champs de clé hello que vous utiliserez dans cette application de la détection des fraudes en temps réel sont suivant de hello :

|**Enregistrement**|**Définition**|
|----------|--------------|
|`CallrecTime`|heure de début timestamp Hello pour l’appel de hello. |
|`SwitchNum`|commutateur de téléphone Hello utilisé appel de hello tooconnect. Pour cet exemple, les commutateurs hello sont des chaînes qui représentent des pays hello d’origine (des États-Unis, en Chine, Royaume-Uni, en Allemagne ou Australie). |
|`CallingNum`|numéro de téléphone de Hello d’appelant de hello. |
|`CallingIMSI`|Hello identité imsi (International Mobile Subscriber Identity). Il s’agit d’identificateur Unique de hello de l’appelant de hello. |
|`CalledNum`|numéro de téléphone Hello du destinataire de l’appel hello. |
|`CalledIMSI`|Identité de l'abonné mobile international (IMSI). Il s’agit d’identificateur unique de hello du destinataire de l’appel hello. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>Créer un toomanage de travail Analytique de flux en continu de données

Maintenant que vous disposez d’un flux des événements d’appel, vous pouvez configurer un travail Stream Analytics. travail de Hello lisent les données de concentrateur d’événements hello que vous avez configurée. 

### <a name="create-hello-job"></a>Créer le travail de hello 

1. Bonjour portail Azure, cliquez sur **nouveau** > **Internet of Things** > **tâche de flux de données Analytique**.

2. Nom du travail hello `sa_frauddetection_job_demo`, spécifiez un abonnement, le groupe de ressources et l’emplacement.

    Il s’agit d’une bonne idée tooplace hello hello et travail de concentrateur d’événements Bonjour même région pour meilleures performances et que vous ne payez tootransfer données entre les régions.

    ![Créer un travail Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. Cliquez sur **Créer**.

    Hello travail est créé et le portail de hello affiche les détails de la tâche. Rien n’est en cours d’exécution, cependant, vous avez une tâche de hello tooconfigure avant de pouvoir être démarré.

### <a name="configure-job-input"></a>Configurer les entrées du travail

1. Dans le tableau de bord hello ou hello **toutes les ressources** panneau, recherchez et sélectionnez hello `sa_frauddetection_job_demo` tâche de flux de données Analytique. 
2. Bonjour **travail topologie** section Hello Panneau de tâche Analytique de flux de données, cliquez sur hello **entrée** boîte.

    ![Zone d’entrée sous la topologie dans le panneau de tâche hello Analytique de diffusion en continu](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. Cliquez sur  **+ &nbsp;ajouter** puis remplissez panneau hello avec ces valeurs :

    * **Alias d’entrée**: utiliser le nom hello `CallStream`. Si vous utilisez un autre nom, prenez-en note, car vous en aurez besoin ultérieurement.
    * **Type de source** : sélectionnez **Flux de données**. (**Données de référence** fait référence à des données de recherche de toostatic, que vous n’utilisez pas dans ce didacticiel.)
    * **Source** : sélectionnez **Event Hub**.
    * **Option d’importation** : sélectionnez **Utiliser le hub d’événements de l’abonnement actuel**. 
    * **Espace de noms service bus**: sélectionnez hello événement hub namespace que vous avez créé précédemment (`<yourname>-eh-ns-demo`).
    * **Concentrateur d’événements**: concentrateur d’événements hello Select que vous avez créé précédemment (`sa-eh-frauddetection-demo`).
    * **Nom de la stratégie hub événement**: sélectionnez la stratégie d’accès hello que vous avez créé précédemment (`sa-policy-manage-demo`).

    ![Créer une entrée pour le travail Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. Cliquez sur **Créer**.

## <a name="create-queries-tootransform-real-time-data"></a>Créer des requêtes tootransform des données en temps réel

À ce stade, vous avez une tâche de flux de données Analytique configurer tooread un flux de données entrantes. étape suivante de Hello est toocreate une transformation qui analyse les données hello en temps réel. Pour ce faire, créez une requête. Stream Analytics prend en charge un modèle de requête simple et déclaratif pour la description des transformations dans le cadre du traitement en temps réel. les requêtes de Hello utilisent un langage de type SQL qui a certaines analytique de toostream spécifique d’extensions. 

Une requête très simple peut-être lire simplement toutes les données entrantes hello. Toutefois, vous souvent créez des requêtes qui recherchent des données spécifiques ou pour les relations dans les données de salutation. Dans cette section du didacticiel de hello, vous créer et tester plusieurs requêtes toolearn dans lequel vous pouvez transformer un flux d’entrée pour l’analyse de plusieurs façons. 

vous créez ici des requêtes Hello affiche simplement écran de toohello de données transformées hello. Dans une section ultérieure, vous allez configurer un récepteur de sortie et une requête qui écrit hello données transformées toothat récepteur.

toolearn en savoir plus sur le langage de hello, consultez hello [référence du langage de requête Azure Stream Analytique](https://msdn.microsoft.com/library/dn834998.aspx).

### <a name="get-sample-data-for-testing-queries"></a>Obtenir des exemples de données pour tester des requêtes

application de TelcoGenerator Hello envoie concentrateur d’événements toohello appel enregistrements, et votre tâche de flux de données Analytique est tooread configuré à partir du concentrateur d’événements hello. Vous pouvez utiliser un toomake de travail requête tootest hello certain lire correctement. trop de tester une requête Bonjour console Azure, vous avez besoin d’exemples de données. Pour cette procédure pas à pas, vous allez extraire les exemples de données à partir de flux hello qui sera disponible dans le concentrateur d’événements hello.

1. Assurez-vous que cette application de TelcoGenerator hello est en cours d’exécution et produire des enregistrements de l’appel.
2. Dans le portail hello, retourner le panneau de tâche toohello Analytique de diffusion en continu. (Si vous avez fermé le panneau de hello, recherchez `sa_frauddetection_job_demo` Bonjour **toutes les ressources** panneau.)
3. Cliquez sur hello **requête** boîte. Azure répertorie les entrées hello et sorties qui sont configurés pour la tâche de hello et vous permet de créer une requête qui vous permet de transforment les flux d’entrée hello lors de leur envoi toohello sortie.
4. Bonjour **requête** panneau, cliquez sur toohello suivant de points hello `CallStream` d’entrée, puis sélectionnez **les exemples de données à partir de l’entrée**.

    ![Menu options toouse exemples de données pour hello Analytique de diffusion en continu de la tâche entrée, « Exemples de données à partir de l’entrée « sélectionné](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Cette opération ouvre un panneau qui vous permet de spécifier la quantité tooget de données d’exemple, définie en termes de la durée pendant laquelle le flux d’entrée tooread hello.

5. Définissez **Minutes** too3 puis cliquez sur **OK**. 
    
    ![Options d’échantillonnage de flux d’entrée de hello, avec « 3 minutes » sélectionnées.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure échantillonne les données du flux d’entrée de hello sur 3 minutes et vous avertit lorsque les données d’exemple hello sont prêtes. (Cette opération prend quelques instants.) 

Hello exemples de données sont stockées temporairement et sont disponibles tant que fenêtre de requête hello ouvert. Si vous fermez la fenêtre de requête hello, les données d’exemple hello sont ignorées, et vous aurez toocreate un nouvel ensemble d’exemples de données. 

En guise d’alternative, vous pouvez obtenir un fichier .json qui comporte des exemples de données en [à partir de GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json), puis téléchargez ce toouse de fichier .json en tant qu’exemples de données pour hello `CallStream` d’entrée. 

### <a name="test-using-a-pass-through-query"></a>Procéder à un test à l’aide d’une requête directe

Si vous souhaitez tooarchive chaque événement, vous pouvez utiliser une requête directe de tooread tous les champs hello dans la charge utile de hello d’événement de hello.

1. Dans la fenêtre de requête hello, entrez cette requête :

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >Comme dans SQL, les mots clés ne respectent pas la casse, et les espaces blancs ne sont pas significatifs.

    Dans cette requête, `CallStream` est hello alias que vous avez spécifié lorsque vous avez créé l’entrée de hello. Si vous en avez utilisé un autre, utilisez plutôt ce nom.

2. Cliquez sur **Test**.

    tâche de flux de données Analytique Hello exécute la requête de hello sur des données d’exemple hello et affiche la sortie de hello bas hello de fenêtre hello. Vous pouvez en déduire que concentrateur d’événements hello et le travail de diffusion en continu d’Analytique hello sont correctement configurés. (Comme indiqué, plus tard vous allez créer un récepteur de sortie que hello requête peut écrire les données.)

    ![Sortie du travail Stream Analytics, affichant 73 enregistrements générés](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    nombre exact de Hello d’enregistrements que vous voyez dépend du nombre d’enregistrements qui ont été capturé dans votre exemple de 3 minutes.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>Réduire le nombre de hello de champs à l’aide d’une projection de colonne

Dans de nombreux cas, l’analyse n’a pas besoin de toutes les colonnes hello hello flux d’entrée. Vous pouvez utiliser un tooproject requête un plus petit jeu de retourné de champs que dans les requêtes pass-through hello.

1. Modifier la requête hello dans hello code éditeur toohello suivant :

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. Cliquez de nouveau sur **Test**. 

    ![Sortie du travail Stream Analytics pour la projection, affichant 25 enregistrements générés](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>Compter les appels entrants par région : fenêtre bascule avec agrégation

Supposons que vous souhaitiez toocount hello quantité, pour les appels entrants par région. Dans le flux de données, lorsque vous souhaitez tooperform les fonctions d’agrégation telles que l’inventaire, il faut toosegment hello flux en unités temporelles (étant donné que les flux de données hello lui-même est efficacement sans fin). Pour ce faire, utilisez une [fonction de fenêtre](stream-analytics-window-functions.md) Stream Analytics. Ensuite, vous pouvez travailler avec des données à l’intérieur de cette fenêtre hello en tant qu’unité.

Pour cette transformation, vous souhaitez une séquence de fenêtres temporelles ne se chevauchant pas ; chaque fenêtre contient un ensemble distinct de données que vous pouvez regrouper et agréger. Ce type de fenêtre est tooas auxquels un *fenêtre bascule* . Dans la fenêtre bascule de hello, vous pouvez obtenir un nombre d’appels entrants à hello regroupés par `SwitchNum`, qui représente hello du pays où les appels hello. 

1. Modifier la requête hello dans hello code éditeur toohello suivant :

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    Cette requête utilise hello `Timestamp By` mot clé Bonjour `FROM` toospecify clause quel champ timestamp Bonjour d’entrée de fenêtre bascule de flux toouse toodefine hello. Dans ce cas, fenêtre hello divise les données de salutation en segments par hello `CallRecTime` champ dans chaque enregistrement. (Si aucun champ n’est spécifié, opération de fenêtrage hello utilise heure hello que chaque événement arrive sur le concentrateur d’événements hello. Voir « Heure d’arrivée par rapport à l’heure de l’application » dans [Informations de référence sur le langage de requête Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx). 

    projection de Hello inclut `System.Timestamp`, qui retourne un horodatage de fin hello de chaque fenêtre. 

    toospecify que vous souhaitez toouse une fenêtre bascule, vous utilisez hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) fonction Bonjour `GROUP BY `clause. Dans la fonction hello, vous spécifiez une unité de temps (n’importe où à partir d’un jour de tooa microsecondes) et une taille de fenêtre (le nombre d’unités). Dans cet exemple, la fenêtre bascule de hello se compose d’intervalles de 5 secondes, afin de vous obtiendrez un nombre par pays pour la valeur de chaque 5 secondes d’appels.

2. Cliquez de nouveau sur **Test**. Dans les résultats de hello, notez que des horodateurs hello sous **WindowEnd** sont présentés par incréments de 5 secondes.

    ![Sortie du travail Stream Analytics pour l’agrégation, affichant 13 enregistrements générés](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>Détecter une fraude à la carte SIM à l’aide d’une jointure réflexive

Pour cet exemple, nous pouvons envisager l’utilisation frauduleuse toobe appels provenant de hello même utilisateur, mais dans différents emplacements dans les 5 secondes, une de l’autre. Par exemple, hello même utilisateur ne peut pas légitimement effectuer un appel à partir de hello des États-Unis et de l’Australie au hello même temps. 

toocheck pour ces cas, vous pouvez utiliser une jointure réflexive de hello de diffusion en continu de données toojoin hello flux tooitself selon hello `CallRecTime` valeur. Vous pouvez ensuite rechercher pour l’appel des enregistrements où hello `CallingIMSI` valeur (hello numéro d’origine) est hello identiques, mais hello `SwitchNum` valeur (pays d’origine) n’est pas hello identiques.

Lorsque vous utilisez une jointure avec la diffusion en continu de données, jointure de hello doit fournir des limitations hello décalage qui correspondent aux lignes peuvent être séparées dans le temps. (Comme indiqué précédemment, hello de diffusion en continu de données est effectivement sans fin.) limites de temps Hello pour la relation de hello sont spécifiés à l’intérieur de hello `ON` clause de jointure hello, à l’aide de hello `DATEDIFF` (fonction). Dans ce cas, jointure de hello est basée sur un intervalle de 5 secondes de données d’appel.

1. Modifier la requête hello dans hello code éditeur toohello suivant : 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    Cette requête est comme toute autre jointure SQL à l’exception de hello `DATEDIFF` fonction dans la jointure de hello. Il s’agit d’une version de `DATEDIFF` tooStreaming spécifique Analytique, et il doit s’afficher dans hello `ON...BETWEEN` clause. paramètres de Hello sont une unité de temps (en secondes dans cet exemple) et les alias de hello de deux sources de hello pour la jointure de hello. (Ceci diffère hello SQL standard `DATEDIFF` fonction.) 

    Hello `WHERE` clause inclut condition hello qui signale les appel frauduleux hello : les commutateurs d’origine hello ne sont pas hello identiques. 

2. Cliquez de nouveau sur **Test**. 

    ![Sortie du travail Stream Analytics pour la jointure réflexive, affichant 6 enregistrements générés](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. Cliquez sur **Enregistrer**. Cela enregistre la requête de jointure réflexive hello en tant que partie du travail de diffusion en continu d’Analytique hello. (Il n’enregistre pas les données d’exemple hello).

    ![Enregistrer un travail Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>Créer un récepteur de sortie transformé de toostore données

Vous avez défini un flux d’événements, un tooingest d’entrée de concentrateur d’événements et une requête de tooperform une transformation sur les flux hello. dernière étape de Hello est toodefine récepteur de sortie pour le travail de hello : autrement dit, un Bonjour de toowrite place transformés flux à. 

Vous pouvez utiliser de nombreuses ressources comme récepteurs de sortie : une base de données SQL Server, le stockage Table, le stockage Data Lake, Power BI et même un autre concentrateur Event Hub. Pour ce didacticiel, vous allez écrire hello flux tooAzure stockage d’objets Blob, qui est un choix par défaut pour la collecte des informations sur les événements pour une analyse ultérieure, car il prend en charge des données non structurées.

Si vous possédez déjà un compte de stockage d’objets blob, vous pouvez l’utiliser. Pour ce didacticiel, nous allons vous montrer comment toocreate un nouveau compte de stockage juste pour ce didacticiel.

### <a name="create-an-azure-blob-storage-account"></a>Créer un compte de stockage Blob Azure

1. Bonjour portail Azure, retourner le panneau de tâche toohello Analytique de diffusion en continu. (Si vous avez fermé le panneau de hello, recherchez `sa_frauddetection_job_demo` Bonjour **toutes les ressources** panneau.)
2. Bonjour **travail topologie** , cliquez sur hello **sortie** boîte. 
3. Bonjour **sorties** panneau, cliquez sur  **+ &nbsp;ajouter** puis remplissez panneau hello avec ces valeurs :

    * **Alias de sortie**: utiliser le nom hello `CallStream-FraudulentCalls`. 
    * **Sink** : sélectionnez **Stockage d’objets blob**.
    * **Options d’importation** : sélectionnez **Utiliser l’objet blob de stockage de l’abonnement actuel**.
    * **Compte de stockage** : sélectionnez **Créer un compte de stockage**.
    * **Compte de stockage** (seconde zone) : entrez `YOURNAMEsademo`, où `YOURNAME` représente votre nom ou une autre chaîne unique. nom de Hello peut utiliser que des lettres minuscules et des chiffres, et il doit être unique dans Azure. 
    * **Conteneur** : Entrez `sa-fraudulentcalls-demo`.
    nom de compte de stockage Hello et le nom de conteneur sont tooprovide ensemble utilisé un URI pour le stockage d’objets blob hello, comme suit : 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Panneau Nouvelle sortie pour le travail Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. Cliquez sur **Créer**. 

    Azure crée le compte de stockage hello et génère une clé automatiquement. 

5. Fermer hello **sorties** panneau. 

## <a name="start-hello-streaming-analytics-job"></a>Démarrer le travail de diffusion en continu d’Analytique hello

Hello travail est maintenant configuré. Vous avez spécifié une entrée (concentrateur d’événements hello), une transformation (toolook de requête hello pour les appels frauduleux) et une sortie (stockage d’objets blob). Vous pouvez maintenant démarrer le travail de hello. 

1. Vérifiez que hello TelcoGenerator application est en cours d’exécution.

2. Dans le panneau de tâche hello, cliquez sur **Démarrer**.

    ![Démarrer la tâche de flux de données Analytique hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. Bonjour **Start job** panneau, pour le travail sortie heure de début, sélectionnez **maintenant**. 

4. Cliquez sur **Start**. 

    ![Panneau de « Démarrer le travail » pour la tâche de flux de données Analytique hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure vous avertit de hello le travail a démarré, et dans le panneau de tâche hello, hello état affiché est **en cours d’exécution**.

    ![État du travail Stream Analytics En cours d’exécution](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>Examiner les données de hello transformé

À présent, vous disposez d’un travail Stream Analytics complet. Hello tâche est examen d’un flux de métadonnées de l’appel téléphonique, recherchez les appels téléphoniques frauduleux en temps réel et l’écriture des informations sur ces toostorage appels frauduleuses. 

toocomplete ce didacticiel, vous souhaiterez peut-être toolook données hello capturés par le travail de diffusion en continu d’Analytique hello. les données de salutation sont écrit tooAzure stockage d’objets BLOB en segments (fichiers). Vous pouvez utiliser n’importe quel outil pour lire Stockage Blob Azure. Comme indiqué dans la section conditions préalables de hello, vous pouvez utiliser des extensions Azure dans Visual Studio, ou vous pouvez utiliser un outil tel que [Azure Storage Explorer](http://storageexplorer.com/) ou [Explorateur Azure](http://www.cerebrata.com/products/azure-explorer/introduction). 

Lorsque vous examinez le contenu de hello d’un fichier dans le stockage blob, vous voyez quelque chose comme hello suivantes :

![Stockage d’objets blob Azure avec sortie Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>Supprimer des ressources

Nous avons des articles supplémentaires qu’elles restent avec le scénario de détection des fraudes hello et qui utilisent des ressources hello que vous avez créé dans ce didacticiel. Si vous souhaitez toocontinue, consultez les suggestions hello sous **étapes** plus tard.

Toutefois, si vous avez terminé et que vous n’avez pas besoin des ressources hello que vous avez créé, vous pouvez les supprimer afin que vous ne subissez inutiles Azure facture. Dans ce cas, nous vous suggérons de que vous hello suivant :

1. Arrêter le travail de diffusion en continu d’Analytique hello. Bonjour **travaux** panneau, cliquez sur **arrêter** haut hello.
2. Arrêt de l’application du Générateur de télécommunications hello. Dans la fenêtre de commande hello où vous avez démarré l’application hello, appuyez sur Ctrl + C.
3. Si vous avez créé un compte de stockage d’objets blob pour ce didacticiel, supprimez-le. 
4. Supprimer le travail de diffusion en continu d’Analytique hello.
5. Supprimer un concentrateur d’événements hello.
6. Supprimer l’espace de noms hello événement hub.

## <a name="get-support"></a>Obtenir de l'aide

Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez poursuivre ce didacticiel hello suivant des articles :

* [Stream Analytics et Power BI : tableau de bord d’analyse en temps réel pour les données de streaming](stream-analytics-power-bi-dashboard.md). Cet article vous explique comment toosend hello sortie télécommunications de hello Analytique de flux de travail tooPower BI pour l’analyse et de visualisation en temps réel.
* [Comment toostore des données à partir de l’Analytique des flux de données Azure dans un Cache Redis Azure à l’aide des fonctions d’Azure](stream-analytics-functions-redis.md). Cet article explique comment toowrite des fonctions d’Azure toouse frauduleux appelle tooan Azure Redis cache via une file d’attente Service Bus.

Pour plus d’informations sur Stream Analytics en général, consultez les articles suivants :

* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
