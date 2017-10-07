---
title: "aaaDiagnose et résoudre les problèmes | Documents Microsoft"
description: "Ce didacticiel décrit comment toodiagnose et résoudre les problèmes dans votre environnement un aperçu en temps série"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Diagnostiquer et résoudre les problèmes dans votre environnement Time Series Insights

## <a name="i-dont-see-my-data"></a>Mes données ne s’affichent pas
Voici quelques raisons pour lesquelles vous ne voyiez pas vos données dans votre environnement Bonjour [portail Azure temps série Insights](https://insights.timeseries.azure.com).

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>Votre source d’événement ne contient pas de données au format JSON
Pour le moment, Azure Time Series Insights ne prend en charge que les données JSON. Pour obtenir des exemples de données JSON, consultez [Structures JSON prises en charge](time-series-insights-send-events.md#supported-json-shapes).

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>Lorsque vous avez inscrit votre source d’événements, vous n’avez pas fourni de clé hello qui a l’autorisation de hello requis
* Pour un hub IoT, vous devez clé hello tooprovide a **service de se connecter** autorisation.

   ![Autorisation de connexion de service IoT Hub](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Comme indiqué dans hello précédant l’image, une des stratégies de hello **iothubowner** et **service** fonctionne, car les deux ont **service de se connecter** autorisation.
* Pour un concentrateur d’événements, vous devez clé hello tooprovide a **écouter** autorisation.

   ![Autorisation d’écoute EventHub](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Comme indiqué dans hello précédant l’image, une des stratégies de hello **lire** et **gérer** fonctionne, car les deux ont **écouter** autorisation.

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>Hello fourni le groupe de consommateurs n’est pas exclusive tooTime série Insights
Un hub IoT ou un concentrateur d’événements, lors de l’inscription nous nécessiter un groupe de consommateurs hello toospecify qui doit être utilisé pour la lecture de vos données. Ce groupe de consommateurs ne doit pas être partagé. S’il est partagé, concentrateur d’événements hello sous-jacent déconnecte automatiquement un des lecteurs de hello aléatoirement.

## <a name="i-see-my-data-but-theres-a-lag"></a>Mes données s’affichent, mais avec un décalage
Voici les raisons pour lesquelles pourquoi vous pouvez voir des données partielles dans votre environnement Bonjour [portail temps série Insights](https://insights.timeseries.azure.com).

### <a name="your-environment-is-getting-throttled"></a>Votre environnement est sujet à des limitations
Hello limitation est appliquée en fonction du type de référence (SKU) et la capacité de l’environnement hello. Toutes les sources d’événements dans l’environnement de hello partagent cette capacité. Si la source d’événement hello pour votre hub IoT ou un concentrateur d’événements est effectué un push des données au-delà des limites de hello appliquée, vous consultez un décalage et limitation.

Hello suivant schéma montre un environnement de temps série Insights qui a une référence (SKU) de S1 et une capacité de 3. Cet environnement peut recevoir 3 millions d’événements par jour.

![Capacité actuelle et référence de l’environnement](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Partons du principe que cet environnement est réception des messages à partir d’un concentrateur d’événements avec les taux d’entrée hello illustré hello suivant schéma :

![Exemple de taux d’entrée pour un concentrateur d’événements](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Comme indiqué dans le diagramme de hello, taux d’entrée quotidien hello est ~ 67 000 messages. Ce taux convertit les messages too46 environ toutes les minutes. Si chaque message d’événement de concentrateur est aplatie tooa événement temps série Insights, cet environnement ne voit aucune limitation. Si chaque message d’événement de concentrateur est aplatie too100 temps série Insights événements, puis 4 600 événements doivent être ingérées toutes les minutes. Un environnement de référence (SKU) S1 qui a une capacité de 3 peut uniquement prendre 2 100 événements d’entrée toutes les minutes (1 million d’événements par jour = 700 événements par minute à 3 unités = 2 100 événements par minute). Par conséquent, vous voyez un décalage toothrottling échéance. 

Pour en savoir plus sur la logique de mise à plat, consultez [Structures JSON prises en charge](time-series-insights-send-events.md#supported-json-shapes).

#### <a name="recommended-steps"></a>Étapes recommandées
retard hello toofix, hello d’augmentation de capacité de référence (SKU) de votre environnement. Pour plus d’informations, consultez [comment tooscale votre environnement temps série Insights](time-series-insights-how-to-scale-your-environment.md).

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>Vous envoyez des données d’historique et causez un ralentissement en entrée
Si vous vous connectez à une source d’événement existante, il est probable que votre concentrateur Event Hub ou IoT Hub comporte déjà des données. Par conséquent, hello démarrage environnement extrayant des données à partir du début hello de période de rétention de message de la source d’événement hello. 

Ce comportement est le comportement par défaut de hello et ne peut pas être substitué. Vous pouvez prendre part aux limitation, et peut prendre un certain temps toocatch haut sur la réception des données d’historique.

#### <a name="recommended-steps"></a>Étapes recommandées
retard hello toofix, hello prennent comme suit :
1. Augmentez hello SKU capacité toohello valeur maximale autorisée (10 dans ce cas). Une fois que la capacité de hello est augmentée, processus d’entrée hello démarre rattrape le retard beaucoup plus rapidement. Vous pouvez visualiser la rapidité avec laquelle vous êtes rattrape le retard via le graphique de disponibilité hello Bonjour [portail temps série Insights](https://insights.timeseries.azure.com). Vous êtes facturé pour la capacité de hello augmenté.
2. Après avoir hello lag est en retard, diminuer les taux d’entrée normal tooyour arrière capacités hello référence (SKU).

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>Le paramètre *Nom de la propriété timestamp* de ma source d’événement ne fonctionne pas
Vérifiez que hello nom et la valeur sont conformes toohello suivant les règles :
* nom de la propriété timestamp Hello est _respectant la casse_.
* valeur de propriété timestamp Hello provenant de votre source d’événement, comme une chaîne JSON, doit avoir le format de hello _AAAA-MM-JJThh. FFFFFFFK_. Exemple de chaîne : 2008-04-12T12:53Z.
