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
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="aa0a1-103">Lire des messages de l’appareil-à-cloud à partir du point de terminaison hello intégrés</span><span class="sxs-lookup"><span data-stu-id="aa0a1-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="aa0a1-104">Par défaut, les messages sont routés toohello intégrés côté service point de terminaison (**messages/événements**), qui est compatible avec [concentrateurs d’événements][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="aa0a1-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="aa0a1-105">Ce point de terminaison est actuellement uniquement exposées à l’aide de hello [AMQP] [ lnk-amqp] protocole sur le port 5671.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="aa0a1-106">Un hub IoT expose hello suivants propriétés tooenable vous toocontrol hello intégré point de terminaison messagerie concentrateur d’événements compatibles **messages/événements**.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="aa0a1-107">Propriété</span><span class="sxs-lookup"><span data-stu-id="aa0a1-107">Property</span></span>            | <span data-ttu-id="aa0a1-108">Description</span><span class="sxs-lookup"><span data-stu-id="aa0a1-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="aa0a1-109">**Nombre de partitions**</span><span class="sxs-lookup"><span data-stu-id="aa0a1-109">**Partition count**</span></span> | <span data-ttu-id="aa0a1-110">Définissez cette propriété au nombre de hello toodefine de la création de [partitions] [ lnk-event-hub-partitions] pour l’ingestion d’événements de l’appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="aa0a1-111">**Durée de rétention**</span><span class="sxs-lookup"><span data-stu-id="aa0a1-111">**Retention time**</span></span>  | <span data-ttu-id="aa0a1-112">Cette propriété spécifie la durée en jours de conservation des messages par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="aa0a1-113">par défaut de Hello est un jour, mais il peut être accrue tooseven jours.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="aa0a1-114">IoT Hub vous permet également de groupes de consommateurs toomanage sur hello intégrés appareil-à-cloud recevoir le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="aa0a1-115">Par défaut, tous les messages qui ne correspondent pas explicitement une règle de routage de message sont écrites toohello de point de terminaison intégrés.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="aa0a1-116">Si vous désactivez cet itinéraire de secours, les messages qui ne correspondent explicitement à aucune règle d’acheminement des messages sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="aa0a1-117">Vous pouvez modifier la durée de rétention hello, que ce soit par programme via hello [fournisseur de ressources IoT Hub API REST][lnk-resource-provider-apis], ou à l’aide de hello [portail Azure] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="aa0a1-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="aa0a1-118">IoT Hub expose hello **messages/événements** messages de périphérique dans le cloud de hello tooread reçus par votre concentrateur de services de point de terminaison prédéfini pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="aa0a1-119">Ce point de terminaison est événement Hub compatibles, qui vous permet de toouse des service Event Hubs de hello mécanismes hello prend en charge pour la lecture des messages.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="aa0a1-120">Lire à partir du point de terminaison hello intégrés</span><span class="sxs-lookup"><span data-stu-id="aa0a1-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="aa0a1-121">Lorsque vous utilisez hello [Azure Service Bus SDK pour .NET] [ lnk-servicebus-sdk] ou hello [concentrateurs d’événements - événements processeur hôte][lnk-eventprocessorhost], vous pouvez utiliser n’importe quelle connexion IoT Hub chaînes avec les autorisations correctes hello.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="aa0a1-122">Utilisez ensuite **messages/événements** comme nom du concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="aa0a1-123">Lorsque vous utilisez les kits de développement logiciel (ou les intégrations de produits) qui ne seront pas informés de IoT Hub, vous devez en récupérer un point de terminaison de Hub d’événements compatibles et le nom du concentrateur d’événements compatibles à partir des paramètres de Hub IoT hello Bonjour [portail Azure] [ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="aa0a1-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="aa0a1-124">Dans le panneau de hello IoT hub, cliquez sur **points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="aa0a1-125">Bonjour **des points de terminaison intégrés** , cliquez sur **événements**.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="aa0a1-126">panneau Hello contient hello valeurs suivantes : **point de terminaison de Hub d’événements compatibles**, **nom du concentrateur d’événements compatibles**, **Partitions**, **la durée de rétention**, et **groupes de consommateurs**.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Paramètres Appareil vers cloud][img-eventhubcompatible]

<span data-ttu-id="aa0a1-128">Hello IoT Hub SDK requiert hello nom de point de terminaison IoT Hub, qui est **messages/événements** comme indiqué dans hello **points de terminaison** panneau.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="aa0a1-129">Si hello Kit de développement logiciel que vous utilisez requiert un **nom d’hôte** ou **Namespace** valeur, supprimez le schéma de hello hello **point de terminaison de Hub d’événements compatibles**.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="aa0a1-130">Par exemple, si votre point de terminaison de Hub d’événements compatibles est **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **nom d’hôte** serait  **iothub-ns-myiothub-1234.servicebus.windows.net**et hello **Namespace** serait **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="aa0a1-131">Vous pouvez ensuite utiliser toute stratégie d’accès partagé qui a hello **ServiceConnect** autorisations tooconnect toohello spécifié concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="aa0a1-132">Si vous devez toobuild une chaîne de connexion du concentrateur d’événements en utilisant les informations précédentes hello, utilisez hello modèle :</span><span class="sxs-lookup"><span data-stu-id="aa0a1-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="aa0a1-133">Kits de développement logiciel Hello et intégrations que vous pouvez utiliser avec points de terminaison de Hub d’événements compatibles IoT Hub expose inclut les éléments de hello Bonjour suivant liste :</span><span class="sxs-lookup"><span data-stu-id="aa0a1-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="aa0a1-134">[Client Event Hubs Java](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="aa0a1-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="aa0a1-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="aa0a1-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="aa0a1-136">Vous pouvez afficher hello [bec source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="aa0a1-137">[Intégration Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="aa0a1-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa0a1-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa0a1-138">Next steps</span></span>

<span data-ttu-id="aa0a1-139">Pour plus d’informations sur les points de terminaison IoT Hub, consultez [Points de terminaison IoT Hub][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="aa0a1-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="aa0a1-140">Hello [prise en main] [ lnk-get-started] didacticiels montrent comment toosend les messages appareil-à-cloud à partir de simulée de périphériques et lire les messages de hello de point de terminaison hello intégrés.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="aa0a1-141">Pour plus d’informations, consultez hello [messages appareil-à-cloud de processus IoT Hub à l’aide d’itinéraires] [ lnk-d2c-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="aa0a1-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="aa0a1-142">Si vous souhaitez tooroute votre appareil-à-cloud messages toocustom de points de terminaison, consultez [utiliser les itinéraires des messages et des points de terminaison personnalisés pour les messages appareil-à-cloud][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="aa0a1-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
