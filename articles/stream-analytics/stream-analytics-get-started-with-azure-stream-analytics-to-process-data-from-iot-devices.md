---
title: "aaaIoT des flux de données en temps réel et Analytique de flux de données Azure | Documents Microsoft"
description: "Flux de données et balises de capteur IoT avec analyses de flux et traitement des données en temps réel"
keywords: "solution IoT, prise en main d’IoT"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>Prise en main avec les données de tooprocess Analytique de flux de données Azure à partir des appareils IoT
Dans ce didacticiel, vous allez apprendre comment toocreate flux-traitement logique toogather des données à partir d’appareils de l’Internet des objets (IoT). Nous allons utiliser un toodemonstrate de cas d’utilisation Internet of Things (IoT) réel, comment toobuild votre solution rapidement et à moindre coût.

## <a name="prerequisites"></a>Composants requis
* [Abonnement Azure](https://azure.microsoft.com/pricing/free-trial/)
* Exemples de fichiers de requête et de données téléchargeables à partir de [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>Scénario
Contoso, qui est une société dans l’espace d’automatisation industrielle hello, automatisées complètement son processus de fabrication. Hello dans cette installation est capteurs compatibles avec l’émission de flux de données en temps réel. Dans ce scénario, un gestionnaire de plancher de production souhaite toohave des informations en temps réel à partir de toolook de données de capteur hello pour les modèles et effectuer des opérations sur les. Nous allons utiliser hello langage de requête Analytique flux (SAQL) sur les modèles intéressants hello capteur données toofind hello flux d’entrée de données.

Dans notre cas, les données sont générées à partir d’un appareil Texas Instruments SensorTag.

![Texas Instruments SensorTag](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

charge utile de Hello de données de hello est au format JSON et l’aspect de hello suivantes :

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

Dans un scénario réel, des centaines de capteurs de ce type pourraient générer des événements sous forme de flux. Dans l’idéal, un périphérique de passerelle exécuterait code toopush ces événements trop[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) ou [Azure IoT Hubs](https://azure.microsoft.com/services/iot-hub/). Votre tâche de flux de données Analytique serait ces événements à partir des concentrateurs d’événements de réception et exécuter des requêtes de l’analytique en temps réel sur les flux hello. Ensuite, vous pouvez envoyer tooone de résultats hello Hello [prise en charge des sorties](stream-analytics-define-outputs.md).

Pour plus de convivialité, ce guide de mise en route fournit un exemple de fichier de données capturé à partir de balises de capteur réelles. Vous pouvez exécuter des requêtes sur les données d’exemple hello et consultez les résultats. Dans les didacticiels suivants, vous allez apprendre comment tooconnect votre tooinputs et les sorties de la tâche et de les déployer toohello service Azure.

## <a name="create-a-stream-analytics-job"></a>Création d’un travail Stream Analytics
1. Bonjour [portail Azure](http://portal.azure.com), cliquez sur le signe plus hello, puis tapez **STREAM ANALYTICS** dans hello texte fenêtre toohello vers la droite. Puis sélectionnez **tâche de flux de données Analytique** dans la liste des résultats hello.
   
    ![Créer une tâche Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. Entrez un nom unique de la tâche et vérifiez l’abonnement de hello est hello un approprié pour votre travail. Ensuite, créez un groupe de ressources ou sélectionnez un groupe existant dans votre abonnement.
3. Sélectionnez ensuite l’emplacement où vous souhaitez placer la tâche. Pour la vitesse de traitement et de réduire les coûts de transfert de données en sélectionnant hello même emplacement que le groupe de ressources hello et compte de stockage concerné est recommandé.
   
    ![Créer une tâche Stream Analytics - détails](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > Vous devez créer ce compte de stockage une seule fois par région. Ce stockage sera partagé entre toutes les tâches Stream Analytics qui sont créées dans cette région.
   > 
   > 
4. Hello boîte tooplace votre travail sur votre tableau de bord, puis cliquez sur **créer**.
   
    ![création de la tâche en cours](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. Vous devez voir un « déploiement démarré...' affichée dans hello en haut à droite de la fenêtre du navigateur. Bientôt, elle deviendra tooa terminée fenêtre comme indiqué ci-dessous.
   
    ![création de la tâche en cours](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Création d’une requête Azure Stream Analytics
Une fois votre travail est créé tooopen de son temps et créer une requête. Vous pouvez accéder facilement votre travail en cliquant sur la vignette de hello pour celle-ci.

![Titre de la tâche](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

Bonjour **travail topologie** volet cliquez sur hello **requête** zone toogo toohello l’éditeur de requête. Hello **requête** éditeur vous permet de requête tooenter T-SQL qui exécute la transformation de hello sur les données d’événements entrants hello.

![Case de requête](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>Requête : Archiver vos données brutes
forme la plus simple de Hello de requête est une requête directe qui archive toutes les données d’entrée tooits désignés de sortie. Télécharger le fichier de données d’exemple hello de [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) emplacement tooa sur votre ordinateur. 

1. Collez la requête hello à partir du fichier de PassThrough.txt hello. 
   
    ![Flux d’entrée du test](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Cliquez sur entrée tooyour suivante de hello trois points et sélectionnez **télécharger des exemples de données à partir du fichier** boîte.
   
    ![Flux d’entrée du test](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. Un volet s’ouvre sur hello à droite, par conséquent, qu’il contient les données de hello sélectionnez HelloWorldASA-InputStream.json à partir de votre emplacement de téléchargement de fichiers, cliquez sur **OK** bas hello du volet de hello.
   
    ![Flux d’entrée du test](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. Puis cliquez sur hello **Test** ENGRENAGE dans hello zone supérieure gauche de la fenêtre hello et traiter votre requête de test dans le jeu de données exemple hello. Une fenêtre de résultats s’ouvre sous votre requête que le traitement de hello est terminé.
   
    ![Résultats du test](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>Requête : Filtrer les données de hello basées sur une condition
Essayons de résultats de hello toofilter basés sur une condition. Nous aimerions résultats tooshow pour que les événements provenant de « sensorA ». requête de Hello est dans un fichier de Filtering.txt hello.

![Filtrage d’un flux de données](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Notez que cette requête de la casse hello compare la valeur de chaîne. Cliquez sur hello **Test** engrenage à nouveau des requêtes de hello tooexecute. requête de Hello doit retourner des 389 lignes 1860 événements.

![Résultats de la deuxième sortie du test de requête](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>De requête : Tootrigger d’alerte un flux de travail d’entreprise
Nous allons maintenant affiner notre requête. Pour chaque type de capteur, nous souhaitez toomonitor la température moyenne par de 30 secondes et afficher les résultats uniquement si la température moyenne de hello est supérieure à 100 degrés. Nous allons écrire suivant de hello de requête, puis cliquez sur **Test** des résultats toosee hello. requête de Hello est dans un fichier de ThresholdAlerting.txt hello.

![Requête de filtre de 30 secondes](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

Vous devez maintenant voir des résultats qui contiennent des lignes et des noms des capteurs 245 uniquement où moyenne hello températures est supérieure à 100. Cette requête regroupe des flux hello d’événements par **dspl**, qui est supérieure à nom du capteur hello, un **fenêtre bascule** de 30 secondes. Des requêtes temporelles doivent indiquer comment nous souhaitons tooprogress de temps. À l’aide de hello **TIMESTAMP BY** clause, nous avons spécifié hello **OUTPUTTIME** fois tooassociate de colonne avec tous les calculs temporelle. Pour plus d’informations, consultez articles MSDN de hello [gestion du temps](https://msdn.microsoft.com/library/azure/mt582045.aspx) et [fonctions de fenêtrage](https://msdn.microsoft.com/library/azure/dn835019.aspx).

### <a name="query-detect-absence-of-events"></a>Requête : Détection de l’absence d’événements
Comment pouvons-nous nous écrivons une requête toofind un manque d’événements d’entrée ? Nous allons rechercher hello dernière fois qu’un capteur envoyé des données et puis n’a pas envoyé d’événements pour hello prochaine minute. requête de Hello est dans un fichier de AbsenseOfEvent.txt hello.

![Détection de l’absence d’événements](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

Nous utilisons ici un **LEFT OUTER** joindre toohello du flux de données mêmes (jointure réflexive). Pour une jointure **INNER**, un résultat n’est renvoyé que si une correspondance est trouvée.  Pour un **LEFT OUTER** jointure, si un événement à partir de hello à gauche de la jointure de hello est non appariée, une ligne qui a une valeur NULL pour tous les hello colonnes du côté droit de hello est retournée. Cette technique est très utile toofind une absence d’événements. Pour en savoir plus sur [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx), consultez notre documentation MSDN.

## <a name="conclusion"></a>Conclusion
Hello ce didacticiel vise toodemonstrate affichage des résultats de requêtes langage de requête Analytique Stream toowrite et voir dans le navigateur de hello. Toutefois, il ne s’agit que d’une prise en main. Stream Analytics offre de nombreuses autres possibilités. Analytique de flux de données prend en charge une variété d’entrées et sorties, et peut même utiliser les fonctions dans Azure Machine Learning toomake il un outil puissant pour l’analyse des flux de données. Vous pouvez démarrer tooexplore plus d’informations sur les flux de données Analytique à l’aide de notre [parcours d’apprentissage](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/). Pour plus d’informations sur les requêtes toowrite, lisez l’article de hello sur [modèles de requête courants](stream-analytics-stream-analytics-query-patterns.md).

