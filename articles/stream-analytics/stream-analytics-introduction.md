---
title: aaaIntroduction tooStream Analytique | Documents Microsoft
description: "En savoir plus sur les flux de données Analytique, un service géré qui vous permet d’analyser les données de diffusion en continu de hello Internet of Things (IoT) en temps réel."
keywords: "analyse en tant que service, services gérés, traitement des données de diffusion en continu, analyse de diffusion en continu, qu’est-ce que Stream Analytics"
services: stream-analytics
documentationcenter: 
author: jenniehubbard
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/08/2017
ms.author: jhubbard
ms.openlocfilehash: 6dd7ea1d358bcc94e927a3e699a2771a25104d72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-stream-analytics"></a>Qu’est-ce que Stream Analytics ?

Azure Stream Analytics est un moteur de traitement des événements entièrement géré qui vous permet de définir des calculs analytiques en temps réel sur la diffusion des données. les données de salutation peuvent provenir d’appareils, capteurs, sites web, des flux sociaux, applications, systèmes d’infrastructure et bien plus encore. 

## <a name="what-can-i-do-with-stream-analytics"></a>Dans quels cas puis-je utiliser Stream Analytics ?

Utiliser des flux de données Analytique tooexamine grands volumes de données circulant de périphériques ou les processus, extraire des informations de flux de données hello et rechercher des modèles, des tendances et des relations. Basé sur les nouveautés dans les données de salutation, vous pouvez ensuite effectuer des tâches de l’application. Par exemple, vous pourrez déclencher des alertes, déclencher le flux de travail automation, flux tooa informations outil, telles que Power BI reporting ou stocker des données pour un examen ultérieur. 

Exemples :

* Analyse en temps réel et personnalisée de transactions en actions et propositions d’alertes par des sociétés de services financiers.
* Détection des fraudes en temps réel basée sur l’examen des données relatives aux transactions. 
* Services de protection des données et des identités.
* Analyse des données générées par des capteurs et des déclencheurs intégrés à des objets physiques (Internet des objets ou IoT).
* Analyse de parcours Web.
* Applications de gestion de la relation client (CRM), telles que l’émission d’alertes en cas de dégradation de l’expérience client au cours d’une période donnée.

## <a name="how-does-stream-analytics-work"></a>Comment fonctionne Stream Analytics ?

Ce diagramme illustre le pipeline de flux Analytique hello, illustrant la sont ingérées, analysées et données puis envoyées pour la présentation ou l’action. 

![Pipeline Stream Analytics](./media/stream-analytics-introduction/stream_analytics_intro_pipeline.png)

Stream Analytics démarre avec une source de données de diffusion en continu. les données de salutation et peuvent être transférées à partir d’un périphérique à l’aide d’un concentrateur d’événements Azure ou un hub IoT dans Azure. les données de salutation peuvent également être extraites d’un magasin de données tels que le stockage d’objets Blob Azure. 

flux de données tooexamine hello, que vous créez un flux d’Analytique *travail* indiquant d'où proviennent les données de salutation. travail de Hello spécifie également un *transformation*&mdash;comment toolook des données, des modèles ou des relations. Pour cette tâche, Stream Analytics prend en charge un langage de requête de type SQL qui vous permet de filtrer,de trier, d’agréger et de joindre les données de diffusion sur une période donnée.

Enfin, le travail de hello spécifie une sortie toosend transformée les données de salutation à. Cela vous permet de contrôler quels toodo dans les informations de réponse toohello analysé. Par exemple, dans la réponse tooanalysis, vous pouvez :

* Envoyer une commande toochange les paramètres d’un périphérique. 
* Envoyer la file d’attente tooa des données qui est surveillé par un processus qui prend des mesures en fonction de ce qu’il trouve. 
* Envoyer des données tooa tableau de bord de création de rapports.
* Envoyer toostorage de données comme stockage d’objets Blob Azure ou une Table, de la base de données SQL Server ou Data Lake Store.

Vous pouvez surveiller et régler le nombre d’événements traités par seconde lors de l’exécution d’un travail. Vous pouvez également faire en sorte que des travaux produisent des journaux de diagnostic pour la résolution de problèmes.

## <a name="key-capabilities-and-benefits"></a>Avantages et fonctionnalités clés

Flux de données Analytique est toouse facile toobe conçue, travail tooany flexible et évolutive, économique et taille.

### <a name="connectivity-toomany-inputs-and-outputs"></a>Connectivité réduire entrées et sorties

Analytique de flux de données se connecte directement trop[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) et [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) de réception du flux de données et hello [service de stockage d’objets Blob Azure](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage-accounts) tooingest les données d’historique. Si vous obtenez des données à partir de concentrateurs d’événements, vous pouvez associer Stream Analytics à d’autres sources de données et moteurs de traitement.

L’entrée de travail peut également inclure des données de référence (données statiques ou à variation lente). Vous pouvez joindre la diffusion en continu données toothis référence données tooperform recherche opérations hello même façon que vous le feriez avec des requêtes de base de données.

Acheminez la sortie du travail Stream Analytics dans plusieurs directions. Vous pouvez écrire toostorage, tels que les objets BLOB de stockage Azure ou tables, base de données SQL Azure, Azure lac de magasins de données ou base de données Azure Cosmos. À partir de là, les données de salutation peuvent entrer pour l’analytique de lot via Azure HDInsight. Vous pouvez envoyer hello sortie tooanother service pour la consommation par un autre processus, tels que des concentrateurs d’événements, les rubriques du Bus des services Azure ou les files d’attente. Vous pouvez envoyer hello sortie tooPower BI de visualisation.

### <a name="ease-of-use"></a>Simplicité d'utilisation

toodefine transformations, vous utilisez une simple, déclarative [de langage de requête de flux de données Analytique](https://msdn.microsoft.com/library/azure/dn834998.aspx) qui vous permet de créer des analyses complexes sans programmation. langage de requête Hello prend la diffusion en continu de données comme entrée. Vous pouvez ensuite filtrer et trier les données de salutation, agréger des valeurs, effectuer des calculs, joindre des données (au sein d’un flux ou tooreference des données) et utiliser des fonctions géospatiales. Vous pouvez modifier des requêtes dans le portail hello, à l’aide d’IntelliSense et la vérification de la syntaxe, et vous pouvez tester les requêtes à l’aide des exemples de données que vous pouvez extraire à partir de flux live de hello.

### <a name="extensible-query-language"></a>Langage de requête extensible

Vous pouvez étendre les fonctionnalités de hello du langage de requête hello en définissant et en appelant des fonctions supplémentaires. Vous pouvez définir des appels de fonction Bonjour parti de tootake service Azure Machine Learning des solutions d’Azure Machine Learning. Vous pouvez également intégrer JavaScript, fonctions définies par l’utilisateur (UDF) dans des calculs complexes ordre tooperform dans le cadre d’une requête Analytique de flux de données.

### <a name="scalability"></a>Extensibilité

Flux de données Analytique peut gérer des Go too1 des données entrantes par seconde. Intégration avec [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) et [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) permet à quelques tâches tooingest des millions d’événements par seconde provenant de périphériques connectés, les visites et les fichiers de journaux, tooname. À l’aide de la fonction de partition hello des concentrateurs d’événements, vous pouvez partitionner des calculs en étapes logiques, chacune avec hello capacité toobe davantage partitionnées tooincrease évolutivité.

### <a name="low-cost"></a>Faible coût

Comme un service cloud, flux de données Analytique est toolet optimisé, vous commencez à faible coût. Vous payez comme vous accédez en fonction de quantité hello et l’utilisation d’unité de diffusion en continu de données traitées par le système de hello. L’utilisation est dérivée en fonction de volume hello d’événements traités et quantité hello de puissance de calcul configurés dans hello cluster toohandle des tâches de flux de données Analytique.

### <a name="reliability-quick-recovery-and-repeatability"></a>Fiabilité, récupération rapide et répétabilité

Un service géré dans le cloud de hello, Analytique de flux de données permet d’éviter la perte de données et permet la continuité. En cas de panne, le service de hello offre des fonctionnalités de récupération intégrées. Avec possibilité de hello toointernally conserver l’état, le service de hello fournit des résultats reproductibles vous être assuré qu’il est possible tooarchive les événements et réappliquez le traitement dans le futur hello, toujours, obtenir les mêmes résultats hello. Cela vous permet de toogo dans le temps et que vous examinez les calculs lors de la cause profonde, analyse de simulation et ainsi de suite.

## <a name="next-steps"></a>Étapes suivantes

* Commencez par l’[expérimentation d’entrées et de requêtes à partir d’appareils IoT](stream-analytics-get-started-with-azure-stream-analytics-to-process-data-from-iot-devices.md).
* Générer un [solution Analytique de flux de bout en bout](stream-analytics-real-time-fraud-detection.md) qui examine toolook de métadonnées de téléphone pour les appels frauduleuses.
* En savoir plus sur hello langage de requête de type SQL pour Analytique de flux de données et sur les concepts uniques comme [fonctions de fenêtre](stream-analytics-window-functions.md).
* Découvrez comment trop[mettre à l’échelle des tâches de flux de données Analytique](stream-analytics-scale-jobs.md). 
* Découvrez comment trop[intégrer des flux de données Analytique et Azure Machine Learning](stream-analytics-machine-learning-integration-tutorial.md).
* Trouver les réponses aux questions de flux de données Analytique tooyour Bonjour [forum d’Analytique de flux de données Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

