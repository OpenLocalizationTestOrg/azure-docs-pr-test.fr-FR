---
title: "terminaison intégré d’aaaUnderstand hello Azure IoT Hub | Documents Microsoft"
description: "Guide du développeur - décrit comment toouse hello intégrés, les messages appareil-à-cloud de concentrateur d’événements compatibles endpoint toread."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a>Lire des messages de l’appareil-à-cloud à partir du point de terminaison hello intégrés

Par défaut, les messages sont routés toohello intégrés côté service point de terminaison (**messages/événements**), qui est compatible avec [concentrateurs d’événements][lnk-event-hubs]. Ce point de terminaison est actuellement uniquement exposées à l’aide de hello [AMQP] [ lnk-amqp] protocole sur le port 5671. Un hub IoT expose hello suivants propriétés tooenable vous toocontrol hello intégré point de terminaison messagerie concentrateur d’événements compatibles **messages/événements**.

| Propriété            | Description |
| ------------------- | ----------- |
| **Nombre de partitions** | Définissez cette propriété au nombre de hello toodefine de la création de [partitions] [ lnk-event-hub-partitions] pour l’ingestion d’événements de l’appareil-à-cloud. |
| **Durée de rétention**  | Cette propriété spécifie la durée en jours de conservation des messages par IoT Hub. par défaut de Hello est un jour, mais il peut être accrue tooseven jours. |

IoT Hub vous permet également de groupes de consommateurs toomanage sur hello intégrés appareil-à-cloud recevoir le point de terminaison.

Par défaut, tous les messages qui ne correspondent pas explicitement une règle de routage de message sont écrites toohello de point de terminaison intégrés. Si vous désactivez cet itinéraire de secours, les messages qui ne correspondent explicitement à aucune règle d’acheminement des messages sont supprimés.

Vous pouvez modifier la durée de rétention hello, que ce soit par programme via hello [fournisseur de ressources IoT Hub API REST][lnk-resource-provider-apis], ou à l’aide de hello [portail Azure] [ lnk-management-portal].

IoT Hub expose hello **messages/événements** messages de périphérique dans le cloud de hello tooread reçus par votre concentrateur de services de point de terminaison prédéfini pour votre serveur principal. Ce point de terminaison est événement Hub compatibles, qui vous permet de toouse des service Event Hubs de hello mécanismes hello prend en charge pour la lecture des messages.

## <a name="read-from-hello-built-in-endpoint"></a>Lire à partir du point de terminaison hello intégrés

Lorsque vous utilisez hello [Azure Service Bus SDK pour .NET] [ lnk-servicebus-sdk] ou hello [concentrateurs d’événements - événements processeur hôte][lnk-eventprocessorhost], vous pouvez utiliser n’importe quelle connexion IoT Hub chaînes avec les autorisations correctes hello. Utilisez ensuite **messages/événements** comme nom du concentrateur d’événements hello.

Lorsque vous utilisez les kits de développement logiciel (ou les intégrations de produits) qui ne seront pas informés de IoT Hub, vous devez en récupérer un point de terminaison de Hub d’événements compatibles et le nom du concentrateur d’événements compatibles à partir des paramètres de Hub IoT hello Bonjour [portail Azure] [ lnk-management-portal]:

1. Dans le panneau de hello IoT hub, cliquez sur **points de terminaison**.
1. Bonjour **des points de terminaison intégrés** , cliquez sur **événements**. panneau Hello contient hello valeurs suivantes : **point de terminaison de Hub d’événements compatibles**, **nom du concentrateur d’événements compatibles**, **Partitions**, **la durée de rétention**, et **groupes de consommateurs**.

    ![Paramètres Appareil vers cloud][img-eventhubcompatible]

Hello IoT Hub SDK requiert hello nom de point de terminaison IoT Hub, qui est **messages/événements** comme indiqué dans hello **points de terminaison** panneau.

Si hello Kit de développement logiciel que vous utilisez requiert un **nom d’hôte** ou **Namespace** valeur, supprimez le schéma de hello hello **point de terminaison de Hub d’événements compatibles**. Par exemple, si votre point de terminaison de Hub d’événements compatibles est **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **nom d’hôte** serait  **iothub-ns-myiothub-1234.servicebus.windows.net**et hello **Namespace** serait **iothub-ns-myiothub-1234**.

Vous pouvez ensuite utiliser toute stratégie d’accès partagé qui a hello **ServiceConnect** autorisations tooconnect toohello spécifié concentrateur d’événements.

Si vous devez toobuild une chaîne de connexion du concentrateur d’événements en utilisant les informations précédentes hello, utilisez hello modèle :

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

Kits de développement logiciel Hello et intégrations que vous pouvez utiliser avec points de terminaison de Hub d’événements compatibles IoT Hub expose inclut les éléments de hello Bonjour suivant liste :

* [Client Event Hubs Java](https://github.com/hdinsight/eventhubs-client).
* [Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). Vous pouvez afficher hello [bec source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) sur GitHub.
* [Intégration Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les points de terminaison IoT Hub, consultez [Points de terminaison IoT Hub][lnk-endpoints].

Hello [prise en main] [ lnk-get-started] didacticiels montrent comment toosend les messages appareil-à-cloud à partir de simulée de périphériques et lire les messages de hello de point de terminaison hello intégrés. Pour plus d’informations, consultez hello [messages appareil-à-cloud de processus IoT Hub à l’aide d’itinéraires] [ lnk-d2c-tutorial] didacticiel.

Si vous souhaitez tooroute votre appareil-à-cloud messages toocustom de points de terminaison, consultez [utiliser les itinéraires des messages et des points de terminaison personnalisés pour les messages appareil-à-cloud][lnk-custom].

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
