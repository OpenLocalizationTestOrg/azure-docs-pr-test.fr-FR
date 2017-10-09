---
title: "aaaJob mise à l’échelle avec des fonctions d’Analytique de flux de données Azure & AzureML | Documents Microsoft"
description: "Découvrez comment tooproperly l’échelle des travaux de flux de données Analytique (partitionnement, SU la quantité et bien plus encore) lors de l’utilisation des fonctions d’Azure Machine Learning."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>Mettre à l’échelle votre travail Stream Analytics avec des fonctions Azure Machine Learning
Il est souvent très simple tooset d’une tâche de flux de données Analytique et exécuter des exemples de données par son biais. Que devons-nous faire lorsque nous devons toorun hello même travail avec le plus grand volume de données ? Elle nécessite toounderstand comment tooconfigure hello Analytique de flux de travail afin qu’il mettra à l’échelle. Dans ce document, nous nous concentrerons sur les aspects particuliers de hello de mise à l’échelle Analytique de flux de travaux avec des fonctions d’apprentissage. Pour plus d’informations sur les tâches de flux de données Analytique tooscale voir en général l’article de hello [mise à l’échelle des travaux](stream-analytics-scale-jobs.md).

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>Qu’est-ce qu’une fonction Azure Machine Learning dans Stream Analytics ?
Une fonction Machine Learning dans le flux de données Analytique peut être utilisée comme un appel de fonction normal Bonjour langage de requête Analytique de flux de données. Toutefois, derrière la scène de hello, appels de fonction hello sont en fait des demandes de Service Web de Azure Machine Learning. Web de la machine Learning services prennent en charge « traitement par lot » de plusieurs lignes, et qui est appelé mini- lot, Bonjour même web appel d’API de service, tooimprove débit global. Consultez hello suivant des articles pour plus de détails ; [Fonctions azure Machine Learning dans le flux de données Analytique](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/) et [Azure Machine Learning Web Services](../machine-learning/machine-learning-consume-web-services.md).

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>Configurer un travail Stream Analytics avec des fonctions Azure Machine Learning
Lorsque vous configurez une fonction Machine Learning pour la tâche de flux de données Analytique, il y a deux paramètres tooconsider taille de lot hello des appels de fonction Machine Learning hello et hello unités (SUs) configurées pour la tâche de flux de données Analytique hello diffusion en continu. toodetermine hello les valeurs appropriées dans ce cas, tout d’abord une décision entre la latence et le débit, autrement dit, latence de la tâche de flux de données Analytique hello et le débit de chaque SU. SUs peuvent toujours être ajoutés tooa travail tooincrease de débit d’une requête Analytique de flux de données partitionnée correctement, bien que SUs supplémentaires augmente le coût hello du travail de hello en cours d’exécution.

Par conséquent, il est important de toodetermine hello *la tolérance de panne* de latence en cours d’une tâche de flux de données Analytique. Une latence supplémentaire de l’exécution des demandes de service Azure Machine Learning naturellement augmente avec la taille de lot, qui est composée de latence hello de tâche de flux de données Analytique hello. Hello autre part, l’augmentation de taille de lot permet tooprocess de tâche de flux de données Analytique hello * davantage d’événements avec hello *même nombre* de l’apprentissage des demandes de service web. Fréquence à laquelle l’augmentation hello de latence de service web Machine Learning est augmentation linéaire inférieur toohello taille de lot par conséquent, il est important tooconsider hello plus rentable taille de lot pour un service web de Machine Learning dans toute situation donnée. taille de lot Hello par défaut pour le service web de hello demande est comprise entre 1000 et peut être modifié à l’aide de hello [API REST de flux de données Analytique](https://msdn.microsoft.com/library/mt653706.aspx "API REST de flux de données Analytique") ou hello [client PowerShell pour les flux de données Analytique](stream-analytics-monitor-and-manage-jobs-use-powershell.md "client PowerShell pour les flux de données Analytique").

Une fois qu’une taille de lot a été déterminée, quantité hello diffusion en continu d’unités (SUs) peuvent être déterminées, en fonction hello nombre d’événements que fonction hello doit tooprocess par seconde. Pour plus d’informations sur les unités de diffusion en continu, voir [Mise à l’échelle des travaux Stream Analytics](stream-analytics-scale-jobs.md).

En règle générale, il existe 20 connexions simultanées toohello service de web Machine Learning pour chaque 6 SUs, sauf que les travaux de SU 1 et 3 SU obtenez 20 connexions simultanées également.  Par exemple, si le taux de données d’entrée hello est 200 000 événements par seconde et taille de lot hello est considérée par défaut de toohello 1000 hello résultant web service latence de traitement par lots de 1000 événements mini est 200 ms. Cela signifie que toutes les connexions peuvent envoyer des 5 demandes service web de Machine Learning toohello en une seconde. Avec 20 connexions, la tâche de flux de données Analytique hello peut traiter 20 000 événements dans 200 ms et par conséquent de 100 000 événements en une seconde. Par conséquent, tooprocess 200 000 événements par seconde tâche de flux de données Analytique hello doit 40 connexions simultanées, ce qui se présentent too12 SUs. diagramme de Hello ci-dessous illustre les demandes hello à partir de la terminaison de service web Machine Learning toohello de hello flux Analytique travail – toutes 6 SUs dispose de service web de 20 connexions simultanées tooMachine Learning au max.

![Mettre à l’échelle Stream Analytics avec des fonctions Machine Learning - Exemple de 2 travaux](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "Mettre à l’échelle Stream Analytics avec des fonctions Machine Learning - Exemple de 2 travaux")

En général, ***B*** pour la taille de lot, ***L*** hello web service avec une latence à la taille de lot B, en millisecondes, hello débit d’une tâche de flux de données Analytique avec ***N*** SUs est :

![Mettre à l’échelle Stream Analytics avec des fonctions Machine Learning - Formule](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "Mettre à l’échelle Stream Analytics avec des fonctions Machine Learning - Formule")

Une considération supplémentaire peut être hello 'max d’appels simultanés » sur hello côté de service web Machine Learning, il est recommandé de tooset cette valeur maximale de toohello (200 actuellement).

Pour plus d’informations sur ce paramètre, consultez hello [article de mise à l’échelle pour les Services Web Machine Learning](../machine-learning/machine-learning-scaling-webservice.md).

## <a name="example--sentiment-analysis"></a>Exemple – Analyse de sentiments
Hello exemple suivant inclut une tâche de flux Analytique avec analyse des sentiments hello fonction d’apprentissage automatique, comme décrit dans hello [didacticiel d’intégration de flux Analytique Machine Learning](stream-analytics-machine-learning-integration-tutorial.md).

Hello requête est une requête entièrement partitionnée simple suivie hello **sentiment** de fonction, comme indiqué ci-dessous :

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

Envisagez de hello scénario ; avec un débit de 10 000 tweet par seconde, une tâche de flux de données Analytique doit être créée analyse des sentiments tooperform de tweets de hello (événements). 1 SU, cette tâche de flux de données Analytique serait le trafic de hello en mesure de toohandle ? À l’aide de la taille de lot par défaut de hello de 1000 hello doit être en mesure de tookeep haut avec une entrée hello. Hello supplémentaire ajouté la fonction d’apprentissage doit générer pas plus d’une seconde de latence, ce qui est la latence de générales par défaut hello d’analyse des sentiments hello service web Machine Learning (avec une taille de lot par défaut de 1000). la tâche de flux de données Analytique Hello **globale** ou de la latence de bout en bout est en général pas de quelques secondes. Tenir une présentation plus détaillée de cette tâche de flux de données Analytique, *particulièrement* hello des appels de fonction Machine Learning. Taille de lot hello égal à 1000, un débit de 10 000 événements prendra environ 10 requêtes tooweb service. Même avec 1 SU, il existe suffisamment tooaccommodate de connexions simultanées de saisie du trafic.

Mais que se passe-t-il si le taux d’événement d’entrée hello augmente de 100 x et tâche de flux de données Analytique hello doit maintenant tooprocess de 1 000 000 tweet par seconde ? Nous avons deux options :

1. Augmenter la taille de lot hello, ou
2. Événements hello tooprocess des flux d’entrée de hello de partition en parallèle

Avec l’option de première hello, hello travail **latence** augmente.

Hello deuxième SUs plus seraient devez toobe mis en service et par conséquent générer des demandes de service web Machine Learning plus simultanées. Cela signifie que le travail de hello **coût** augmente.

Supposons latence hello d’analyse des sentiments hello service web Machine Learning est 200 ms pour les traitements d’événement 1000 ou en dessous, 250ms pour les lots de 5 000 événements, 300 millisecondes pour les lots de 10 000 événements ou 500 ms pour les lots de 25 000-event.

1. À l’aide de la première option de hello, (**pas** configuration SUs plus), taille de lot hello peut être augmenté trop**25 000**. À son tour ainsi, hello travail tooprocess 1 000 000 événements avec 20 connexions simultanées toohello service web Machine Learning (avec une latence de 500 ms par appel). Par conséquent, hello une latence supplémentaire de la tâche de flux de données Analytique hello en raison de requêtes à fonction toohello sentiment contre hello apprentissage passerait de demandes de service web **200 ms** trop**500 ms**. Toutefois, notez que taille de lot **ne peut pas** être augmenté à l’infini en tant que services web Machine Learning hello nécessite taille de la charge hello d’une demande de 4 Mo ou plus petites web délai d’attente des demandes de service après 100 secondes de l’opération.
2. À l’aide de la deuxième option de hello, taille de lot hello est laissée à 1 000, avec une latence de service web de 200 ms, chaque service web de toohello 20 connexions simultanées est en mesure de tooprocess 1 000 * 20 * 5 événements = 100 000 par seconde. Tooprocess de 1 000 000 événements par seconde, projet de hello serait donc 60 SUs. Première option toohello comparés, Analytique de flux de travail serait alors plus web ensuite traiter les demandes de traitement par lots, génération d’une augmentation des coûts.

Voici une table pour le débit de la tâche de flux de données Analytique hello hello pour SUs différentes et des tailles de lot (en nombre d’événements par seconde).

| Taille de lot (latence Machine Learning) | 500 (200 ms) | 1 000 (200 ms) | 5 000 (250 ms) | 10 000 (300 ms) | 25 000 (500 ms) |
| --- | --- | --- | --- | --- | --- |
| **1 unité de diffusion en continu** |2 500 |5 000 |20 000 |30 000 |50 000 |
| **3 unités de diffusion en continu** |2 500 |5 000 |20 000 |30 000 |50 000 |
| **6 unités de diffusion en continu** |2 500 |5 000 |20 000 |30 000 |50 000 |
| **12 unités de diffusion en continu** |5 000 |10 000 |40 000 |60 000 |100 000 |
| **18 unités de diffusion en continu** |7 500 |15 000 |60 000 |90 000 |150 000 |
| **24 unités de diffusion en continu** |10 000 |20 000 |80 000 |120 000 |200 000 |
| **…** |… |… |… |… |… |
| **60 unités de diffusion en continu** |25 000 |50 000 |200 000 |300 000 |500 000 |

À ce stade, vous devriez déjà avoir une bonne compréhension du mode de fonctionnement des fonctions Machine Learning dans Stream Analytics. Vous probablement également comprendre que les travaux de flux de données Analytique « collecte » des données à partir de sources de données et chaque « pull » renvoie un lot d’événements pour hello tooprocess de tâche de flux de données Analytique. Comment ce modèle d’extraction répercuter les demandes de service web Machine Learning hello ?

En règle générale, nous avons défini pour les fonctions de l’apprentissage de la taille du lot hello sera exactement divisible par le nombre de hello d’événements retournés par chaque tâche de flux de données Analytique « pull ». Lorsque cela se produit hello service web Machine Learning est appelée avec des lots « partielles ». Cette opération est effectuée toonot entraînent la latence du travail supplémentaire surcharge dans les événements de fusion à partir de toopull d’extraction.

## <a name="new-function-related-monitoring-metrics"></a>Nouvelles métriques de surveillance associées aux fonctions
Dans la zone d’analyse d’une tâche de flux de données Analytique de hello, trois mesures liées à la fonction supplémentaires ont été ajoutés. Ils sont des demandes de fonctions, les événements de fonctions et les demandes de fonction a échoué, comme indiqué dans le graphique de hello ci-dessous.

![Mettre à l’échelle Stream Analytics avec des fonctions Machine Learning - Métriques](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "Mettre à l’échelle Stream Analytics avec des fonctions Machine Learning - Métriques")

Hello sont définies comme suit :

**DEMANDES de fonction**: hello du nombre de demandes de fonction.

**ÉVÉNEMENTS de fonctions**: nombre d’événements hello Bonjour fonction des demandes.

**ÉCHECS de demandes de fonction**: hello du nombre de demandes de fonction qui a échoué.

## <a name="key-takeaways"></a>Points clés
toosummarize hello principaux points, dans l’ordre tooscale une tâche de flux Analytique avec des fonctions d’apprentissage, hello éléments suivants en considération :

1. taux d’événements d’entrée Hello
2. Hello au terme de latence pour hello exécute la tâche de flux de données Analytique (et donc de demande de taille de lot hello du service web de Machine Learning hello)
3. Hello configuré SUs Analytique de flux de données et nombre de hello de demandes de service web Machine Learning (hello liés en fonction des frais supplémentaires)

Notre exemple portait sur une requête Stream Analytics entièrement partitionnée. Si vous avez besoin d’une requête plus complexe hello [forum d’Analytique de flux de données Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) est un bon point de départ pour obtenir une aide supplémentaire à partir de l’équipe de flux de données Analytique hello.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur les flux de données Analytique, consultez :

* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
