---
title: "Connexion de données : entrées de flux de données issues d’un flux d’événements | Microsoft Docs"
description: "En savoir plus sur la configuration d’un tooStream de connexion de données Analytique appelé « entrées ». Les données incluent un flux de données de partir d’événements et également des données de référence."
keywords: "flux de données, connexion de données, flux d’événements"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 8155823c-9dd8-4a6b-8393-34452d299b68
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/05/2017
ms.author: samacha
ms.openlocfilehash: be2008f159061c5c9be9d0314c27fa67193e3269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-connection-learn-about-data-stream-inputs-from-events-toostream-analytics"></a>Connexion de données : en savoir plus sur les données entrées du flux d’événements tooStream Analytique
tâche Analytique de flux de données connexion tooa Hello est un flux d’événements à partir d’une source de données, qui est la tâche désignée tooas hello *d’entrée*. Stream Analytics propose une intégration de pointe aux sources de flux de données Azure, notamment [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) et le [stockage Blob Azure](https://azure.microsoft.com/services/storage/blobs/). Ces entrées sources peuvent être de hello même abonnement Azure en tant que votre tâche analytique ou d’un autre abonnement.

## <a name="data-input-types-data-stream-and-reference-data"></a>Types d’entrée de données : flux de données et données de référence.
Données sont envoyées de source de données tooa, il est consommé par la tâche de flux de données Analytique hello et traités en temps réel. Les entrées sont réparties en deux types : les entrées de flux de données et les entrées de données de référence.

### <a name="data-stream-inputs"></a>Entrées de flux de données
Un flux de données est une séquence illimitée d’événements au fil du temps. Les travaux Stream Analytics doivent contenir au moins une entrée de flux de données. Le stockage d’objets blob, Event Hubs et IoT Hub sont pris en charge en tant que sources d’entrée de flux de données. Concentrateurs d’événements sont des flux d’événements toocollect utilisé à partir de plusieurs appareils et services. Il peut s’agir de flux d’activités de réseaux sociaux, d’informations boursières ou de données provenant de capteurs. Les hubs IoT sont toocollect optimisée des données à partir de périphériques connectés dans des scénarios Internet des objets (IoT).  Le stockage d’objets blob peut être utilisé comme source d’entrée pour la réception de données en bloc en tant que flux, par exemple des fichiers journaux.  

### <a name="reference-data"></a>Données de référence
Stream Analytics prend également en charge des entrées appelées *données de référence*. Ces données auxiliaires sont statiques ou sont modifiées lentement. Elles sont généralement utilisées pour effectuer une corrélation et des recherches. Par exemple, vous pouvez joindre des données dans toodata d’entrée des flux de données hello dans les données de référence hello, que vous pouvez effectuer un toolook de jointure SQL des valeurs statiques. Stockage d’objets Blob Azure est actuellement hello pris en charge uniquement la source d’entrée pour les données de référence. Objets BLOB sources de données de référence sont limités too100 Mo.

toolearn comment afficher les entrées de données de référence toocreate, [utiliser les données de référence](stream-analytics-use-reference-data.md).  

## <a name="create-data-stream-input-from-event-hubs"></a>Créer une entrée de flux de données à partir de concentrateurs Event Hubs

Azure Event Hubs fournit des services de réception d’événements de publication/d’abonnement hautement évolutifs. Un concentrateur d’événements peut collecter des millions d’événements par seconde, afin que vous puissiez traiter et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications. Ensemble, Event Hubs et Stream Analytics vous fournissent une solution complète pour des analyses en temps réel : Event Hubs vous permet d’alimenter Azure en événements en temps réel, et les travaux Stream Analytics peuvent les traiter en temps réel. Par exemple, vous pouvez envoyer les clics sur le web, les lectures des capteurs ou en ligne de journal des événements tooEvent concentrateurs. Vous pouvez ensuite créer des travaux de flux de données Analytique toouse concentrateurs d’événements sous forme de flux de données d’entrée hello pour en temps réel, le filtrage d’agrégation et la corrélation.

horodatage de par défaut de Hello d’événements provenant des Hubs d’événements dans le flux de données Analytique est timestamp hello qui hello événements reçus dans le concentrateur d’événements hello, qui est `EventEnqueuedUtcTime`. tooprocess hello des données en tant que flux à l’aide d’un horodatage dans la charge utile d’événement hello, vous devez utiliser hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) (mot clé).

### <a name="consumer-groups"></a>Groupes de consommateurs
Vous devez configurer chaque toohave d’entrée du concentrateur d’événements Analytique de flux de données à son propre groupe de consommateurs. Lorsqu’un travail contient une jointure réflexive ou s’il comporte plusieurs entrées, une entrée peut être lue par plusieurs lecteurs en aval. Cette situation a un impact sur les nombre hello de lecteurs dans un groupe de consommateurs unique. limite de tooavoid excédant hello concentrateurs d’événements de cinq lecteurs par groupe de consommateurs par partition, elle est une meilleure toodesignate de pratique un consommateur de groupe pour chaque tâche de flux de données Analytique. Il existe également une limite de 20 groupes de consommateurs par concentrateur Event Hub. Pour plus d’informations, consultez l’article [Guide de programmation de concentrateurs d’événements](../event-hubs/event-hubs-programming-guide.md).

### <a name="configure-an-event-hub-as-a-data-stream-input"></a>Configurer un concentrateur Event Hub comme entrée de flux de données
Hello tableau suivant décrit chaque propriété Bonjour **nouvelle entrée** panneau Bonjour portail Azure lorsque vous configurez un concentrateur d’événements en tant qu’entrée.

| Propriété | Description |
| --- | --- |
| **Alias d’entrée** |Un nom convivial que vous utilisez dans tooreference de requête de la tâche hello cette entrée. |
| **Espace de noms Service Bus** |Espace de noms Azure Service Bus, qui est un conteneur pour un ensemble d’entités de messagerie. Lorsque vous créez un concentrateur Event Hub, vous créez également un espace de noms Service Bus. |
| **Nom du hub d’événements** |nom de Hello de toouse de concentrateur d’événements hello en tant qu’entrée. |
| **Nom de la stratégie du hub d’événements** |Bonjour la stratégie d’accès partagé qui fournit le concentrateur d’événements toohello accès. Chaque stratégie d’accès partagé a un nom, les autorisations que vous définissez ainsi que des clés d’accès. |
| **Groupe de consommateurs du hub d’événements** (facultatif) |données de tooingest toouse Hello consommateur groupe à partir du concentrateur d’événements hello. Si aucun groupe de consommateurs n’est spécifié, la tâche de flux de données Analytique hello utilise groupe de consommateurs par défaut hello. Nous vous recommandons d’utiliser un groupe de consommateurs différent pour chaque travail Stream Analytics. |
| **Format de sérialisation de l’événement** |Hello format de sérialisation (JSON, CSV ou Avro) du flux de données entrant hello. |
| **Encodage** | UTF-8 est actuellement de format d’encodage hello uniquement pris en charge. |

Si vos données proviennent d’un concentrateur d’événements, vous avez toohello d’accès suivant dans votre requête Analytique de flux de données des champs de métadonnées :

| Propriété | Description |
| --- | --- |
| **EventProcessedUtcTime** |hello date et heure de cet événement hello a été traité par flux de données Analytique. |
| **EventEnqueuedUtcTime** |hello date et heure de cet événement hello a été reçu par les concentrateurs d’événements. |
| **PartitionId** |ID de partition de base zéro de Hello pour l’adaptateur d’entrée hello. |

Par exemple, à l’aide de ces champs, vous pouvez écrire une requête telle que hello l’exemple suivant :

````
SELECT
    EventProcessedUtcTime,
    EventEnqueuedUtcTime,
    PartitionId
FROM Input
````

## <a name="create-data-stream-input-from-iot-hub"></a>Créer une entrée de flux de données à partir de IoT Hub
Azure Iot Hub est un service de réception d’événements de publication/d’abonnement hautement évolutif optimisé pour les scénarios IoT.

horodatage de par défaut de Hello d’événements provenant d’un IoT hub dans le flux de données Analytique est timestamp hello qui hello événements reçus dans le hub IoT hello, qui est `EventEnqueuedUtcTime`. tooprocess hello des données en tant que flux à l’aide d’un horodatage dans la charge utile d’événement hello, vous devez utiliser hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) (mot clé).

> [!NOTE]
> Seuls les messages envoyés avec une propriété `DeviceClient` peuvent être traités.
> 
> 

### <a name="consumer-groups"></a>Groupes de consommateurs
Vous devez configurer chaque toohave d’entrée de flux de données Analytique IoT hub son propre groupe de consommateurs. Lorsqu’un travail contient une jointure réflexive ou s’il comporte plusieurs entrées, une entrée peut être lue par plusieurs lecteurs en aval. Cette situation a un impact sur les nombre hello de lecteurs dans un groupe de consommateurs unique. limite de tooavoid excédant hello Azure IoT Hub de cinq lecteurs par groupe de consommateurs par partition, elle est une meilleure toodesignate de pratique un consommateur de groupe pour chaque tâche de flux de données Analytique.

### <a name="configure-an-iot-hub-as-a-data-stream-input"></a>Configurer un concentrateur IoT Hub comme entrée de flux de données
Hello tableau suivant décrit chaque propriété Bonjour **nouvelle entrée** panneau Bonjour portail Azure lorsque vous configurez un IoT hub en tant qu’entrée.

| Propriété | Description |
| --- | --- |
| **Alias d’entrée** |Un nom convivial que vous utilisez dans tooreference de requête de la tâche hello cette entrée.|
| **IoT hub** |nom de Hello de hello IoT hub toouse en tant qu’entrée. |
| **Point de terminaison** |point de terminaison Hello pour le hub IoT de hello.|
| **Nom de la stratégie d’accès partagé** |stratégie d’accès Hello partagé qui fournit l’IoT hub toohello de l’accès. Chaque stratégie d’accès partagé a un nom, les autorisations que vous définissez ainsi que des clés d’accès. |
| **Clé de la stratégie d’accès partagé** |clé d’accès partagé Hello utilisé toohello IoT hub tooauthorize accès. |
| **Groupe de consommateurs** (facultatif) |données de tooingest toouse Hello consommateur groupe à partir du hub IoT de hello. Si aucun groupe de consommateurs n’est spécifié, une tâche de flux de données Analytique utilise groupe de consommateurs hello par défaut. Nous vous recommandons d’utiliser un groupe de consommateurs différent pour chaque travail Stream Analytics. |
| **Format de sérialisation de l’événement** |Hello format de sérialisation (JSON, CSV ou Avro) du flux de données entrant hello. |
| **Encodage** |UTF-8 est actuellement de format d’encodage hello uniquement pris en charge. |

Si vos données proviennent d’un hub IoT, vous avez toohello d’accès suivant dans votre requête Analytique de flux de données des champs de métadonnées :

| Propriété | Description |
| --- | --- |
| **EventProcessedUtcTime** |hello date et heure de cet événement hello a été traité. |
| **EventEnqueuedUtcTime** |hello date et heure de cet événement hello a été reçu par IoT hub de hello. |
| **PartitionId** |ID de partition de base zéro de Hello pour l’adaptateur d’entrée hello. |
| **IoTHub.MessageId** | Un ID qui a utilisé la communication bidirectionnelle toocorrelate dans IoT hub. |
| **IoTHub.CorrelationId** |ID utilisé dans les réponses de message et les commentaires dans IoT Hub. |
| **IoTHub.ConnectionDeviceId** |ID de l’authentification de Hello utilisé toosend ce message. Cette valeur est estampillée sur les messages servicebound par IoT hub de hello. |
| **IoTHub.ConnectionDeviceGenerationId** |ID de génération Hello Hello authentifié périphérique qui a été utilisé toosend ce message. Cette valeur est estampillée sur les messages servicebound par IoT hub de hello. |
| **IoTHub.EnqueuedTime** |heure de Hello lorsque le message de salutation a été reçu par IoT hub de hello. |
| **IoTHub.StreamId** |Une propriété d’événement personnalisé ajoutée par l’appareil de l’expéditeur hello. |


## <a name="create-data-stream-input-from-blob-storage"></a>Créer une entrée de flux de données à partir du stockage d’objets blob
Pour les scénarios avec de grandes quantités de toostore des données non structurées dans le cloud de hello, stockage d’objets Blob Azure offre une solution économique et évolutive. Les données du stockage d’objets blob sont généralement considérées comme des données au repos. Toutefois, elles peuvent être traitées comme un flux de données par Stream Analytics. Un scénario classique pour les entrées de stockage d’objets blob avec Stream Analytics correspond au traitement des journaux. Dans ce scénario, les données de télémétrie a été capturées à partir d’un système et des besoins toobe analysée et traitée tooextract des données significatives.

Bonjour timestamp par défaut des événements de stockage Blob dans le flux de données Analytique est timestamp hello qui hello blob a été modifié, ce qui est `BlobLastModifiedUtcTime`. tooprocess hello des données en tant que flux à l’aide d’un horodatage dans la charge utile d’événement hello, vous devez utiliser hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) (mot clé).

Les entrées au format CSV *nécessitent* un toodefine de ligne d’en-tête des champs pour le jeu de données hello. Par ailleurs, tous les champs de ligne d’en-tête doivent être uniques.

> [!NOTE]
> Analytique de flux ne prend pas en charge l’ajout d’objet blob existant de contenu tooan. Flux de données Analytique afficheront un objet blob qu’une seule fois, et toutes les modifications qui se produisent dans l’objet blob de hello après que le travail de hello a lu les données de salutation ne sont pas traitées. Il est recommandé est de tooupload toutes les données hello qu’une seule fois, puis ajoutez de pas magasin d’objets blob toothat événements.
> 

### <a name="configure-blob-storage-as-a-data-stream-input"></a>Configurer un stockage d’objets blob en tant qu’entrée de flux de données

Hello tableau suivant décrit chaque propriété Bonjour **nouvelle entrée** panneau Bonjour portail Azure lorsque vous configurez le stockage d’objets Blob en tant qu’entrée.

| Propriété | Description |
| --- | --- |
| **Alias d’entrée** | Un nom convivial que vous utilisez dans tooreference de requête de la tâche hello cette entrée. |
| **Compte de stockage** | nom Hello hello du compte de stockage dans lequel se trouvent les fichiers d’objets blob hello. |
| **Clé du compte de stockage** | clé secrète de Hello associée au compte de stockage hello. |
| **Conteneur** | conteneur Hello pour l’entrée du blob hello. Les conteneurs fournissent un regroupement logique des objets BLOB stockés dans hello service Microsoft Azure Blob. Lorsque vous téléchargez un objet blob de toohello service de stockage d’objets Blob Azure, vous devez spécifier un conteneur pour cet objet blob. |
| **Modèle de chemin d’accès** (facultatif) | chemin d’accès Hello utilisé des objets BLOB de hello toolocate conteneur hello spécifié. Dans le chemin d’accès de hello, vous pouvez spécifier une ou plusieurs instances de hello suivant trois variables : `{date}`, `{time}`, ou`{partition}`<br/><br/>Exemple 1 : `cluster1/logs/{date}/{time}/{partition}`<br/><br/>Exemple 2 : `cluster1/logs/{date}`<br/><br/>Hello `*` caractère n’est pas une valeur autorisée pour le préfixe de chemin d’accès hello. Seuls les <a HREF="https://msdn.microsoft.com/library/azure/dd135715.aspx">caractères d’objet blob Azure</a> valides sont autorisés. |
| **Format de date** (facultatif) | Si vous utilisez la variable de date hello dans le chemin d’accès de hello, hello dans le hello les fichiers sont organisés de format de date. Exemple : `YYYY/MM/DD` |
| **Format d’heure** (facultatif) |  Si vous utilisez la variable au moment hello dans le chemin d’accès de hello, hello format d’heure dans le hello les fichiers sont organisés. Valeur de hello uniquement pris en charge actuellement est `HH`. |
| **Format de sérialisation de l’événement** | Hello format de sérialisation (JSON, CSV ou Avro) pour les flux de données entrantes. |
| **Encodage** | Pour CSV et JSON, UTF-8 est actuellement de format d’encodage hello uniquement pris en charge. |

Si vos données proviennent d’une source de stockage d’objets Blob, vous avez toohello d’accès suivant dans votre requête Analytique de flux de données des champs de métadonnées :

| Propriété | Description |
| --- | --- |
| **BlobName** |nom Hello d’objet blob d’entrée hello qui hello événement provenait. |
| **EventProcessedUtcTime** |hello date et heure de cet événement hello a été traité par flux de données Analytique. |
| **BlobLastModifiedUtcTime** |hello date et heure de cet objet blob hello a été modifié. |
| **PartitionId** |ID de partition de base zéro de Hello pour l’adaptateur d’entrée hello. |

Par exemple, à l’aide de ces champs, vous pouvez écrire une requête telle que hello l’exemple suivant :

````
SELECT
    BlobName,
    EventProcessedUtcTime,
    BlobLastModifiedUtcTime
FROM Input
````

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
Vous avez appris à connaître les options de connexion de données dans Azure pour vos travaux Stream Analytics. toolearn en savoir plus sur les flux de données Analytique, consultez :

* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
