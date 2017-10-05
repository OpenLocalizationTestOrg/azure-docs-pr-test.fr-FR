---
title: "Comprendre le point de terminaison intégré Azure IoT Hub | Microsoft Docs"
description: "Guide du développeur : décrit comment utiliser le point de terminaison intégré et compatible avec Event Hub pour lire des messages appareil-à-cloud."
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
ms.openlocfilehash: fcc3743028e369fdc42b71887d49fb41fba2c0dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="39254-103">Lire des messages appareil-à-cloud à partir du point de terminaison intégré</span><span class="sxs-lookup"><span data-stu-id="39254-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="39254-104">Par défaut, les messages sont acheminés vers le point de terminaison côté service intégré (**messages/events**) compatible avec [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="39254-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="39254-105">Ce point de terminaison est actuellement uniquement exposé à l’aide du protocole [AMQP][lnk-amqp] sur le port 5671.</span><span class="sxs-lookup"><span data-stu-id="39254-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="39254-106">Un IoT Hub expose les propriétés suivantes pour vous permettre de contrôler le point de terminaison de messages compatible avec Event Hub **messages/events** prédéfini.</span><span class="sxs-lookup"><span data-stu-id="39254-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="39254-107">Propriété</span><span class="sxs-lookup"><span data-stu-id="39254-107">Property</span></span>            | <span data-ttu-id="39254-108">Description</span><span class="sxs-lookup"><span data-stu-id="39254-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="39254-109">**Nombre de partitions**</span><span class="sxs-lookup"><span data-stu-id="39254-109">**Partition count**</span></span> | <span data-ttu-id="39254-110">Configurez cette propriété lors de la création pour définir le nombre de [partitions][lnk-event-hub-partitions] pour la réception d’événements appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="39254-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="39254-111">**Durée de rétention**</span><span class="sxs-lookup"><span data-stu-id="39254-111">**Retention time**</span></span>  | <span data-ttu-id="39254-112">Cette propriété spécifie la durée en jours de conservation des messages par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="39254-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="39254-113">La durée par défaut est de un jour, mais elle peut être augmentée à sept jours.</span><span class="sxs-lookup"><span data-stu-id="39254-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="39254-114">IoT Hub vous permet aussi de gérer des groupes de consommateurs sur le point de terminaison prédéfini de réception appareil vers cloud.</span><span class="sxs-lookup"><span data-stu-id="39254-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="39254-115">Par défaut, tous les messages qui ne correspondent pas explicitement à une règle d’acheminement des messages sont écrits sur le point de terminaison prédéfini.</span><span class="sxs-lookup"><span data-stu-id="39254-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="39254-116">Si vous désactivez cet itinéraire de secours, les messages qui ne correspondent explicitement à aucune règle d’acheminement des messages sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="39254-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="39254-117">La durée de rétention peut être modifiée par programme par le biais des [API REST de fournisseur de ressources IoT Hub][lnk-resource-provider-apis] ou du [Portail Azure][lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="39254-117">You can modify the retention time, either programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="39254-118">IoT Hub expose le point de terminaison prédéfini **messages/events** pour permettre à vos services principaux de lire les messages appareil vers cloud que reçoit votre hub.</span><span class="sxs-lookup"><span data-stu-id="39254-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="39254-119">Ce point de terminaison est compatible avec Event Hub, ce qui vous permet d’utiliser tout mécanisme pris en charge par le service Event Hubs pour la lecture des messages.</span><span class="sxs-lookup"><span data-stu-id="39254-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="39254-120">Lire à partir du point de terminaison intégré</span><span class="sxs-lookup"><span data-stu-id="39254-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="39254-121">Lorsque vous utilisez le [kit SDK Azure Service Bus pour .NET][lnk-servicebus-sdk] ou [l’hôte du processeur d’événements Event Hubs][lnk-eventprocessorhost], vous pouvez utiliser toutes les chaînes de connexion IoT Hub avec les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="39254-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="39254-122">Vous utilisez ensuite **messages/événements** comme nom d’Event Hub.</span><span class="sxs-lookup"><span data-stu-id="39254-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="39254-123">Lorsque vous utilisez des kits SDK ou des intégrations de produits qui n’ont pas connaissance d’IoT Hub, vous devez récupérer un point de terminaison compatible avec Event Hubs et un nom compatible à partir des paramètres IoT Hub dans le [Portail Azure][lnk-management-portal] :</span><span class="sxs-lookup"><span data-stu-id="39254-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from the IoT Hub settings in the [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="39254-124">Dans le panneau IoT Hub, cliquez sur **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="39254-124">In the IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="39254-125">Dans la section **Points de terminaison prédéfinis**, cliquez sur **Événements**.</span><span class="sxs-lookup"><span data-stu-id="39254-125">In the **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="39254-126">Le panneau contient les valeurs suivantes : **Point de terminaison compatible avec Event Hub**, **Nom compatible avec Event Hub**, **Partitions**, **Durée de rétention** et **Groupes de consommateurs**.</span><span class="sxs-lookup"><span data-stu-id="39254-126">The blade contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Paramètres Appareil vers cloud][img-eventhubcompatible]

<span data-ttu-id="39254-128">Le kit SDK IoT Hub requiert le nom de point de terminaison IoT Hub, à savoir **messages/events** comme le montre le panneau **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="39254-128">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown in the **Endpoints** blade.</span></span>

<span data-ttu-id="39254-129">Si le SDK que vous utilisez requiert une valeur **Nom d’hôte** ou **Espace de noms**, supprimez le schéma du **Point de terminaison compatible avec Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="39254-129">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="39254-130">Par exemple, si votre point de terminaison compatible avec les hubs d’événements est **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, le **Nom d’hôte** est **iothub-ns-myiothub-1234.servicebus.windows.net** et l’**Espace de noms** est **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="39254-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and the **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="39254-131">Vous pouvez ensuite utiliser n’importe quelle stratégie d’accès partagé bénéficiant d’autorisations **ServiceConnect** pour vous connecter au Event Hub ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="39254-131">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="39254-132">Si vous devez générer une chaîne de connexion Event Hub en utilisant les informations ci-dessus, vous pouvez utiliser le modèle suivant :</span><span class="sxs-lookup"><span data-stu-id="39254-132">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="39254-133">Les kits SDK et intégrations que vous pouvez utiliser avec les points de terminaison compatibles avec Event Hub exposés par IoT Hub comprennent les éléments de la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="39254-133">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="39254-134">[Client Event Hubs Java](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="39254-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="39254-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="39254-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="39254-136">Vous pouvez afficher la [source spout](https://github.com/apache/storm/tree/master/external/storm-eventhubs) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="39254-136">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="39254-137">[Intégration Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="39254-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="39254-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39254-138">Next steps</span></span>

<span data-ttu-id="39254-139">Pour plus d’informations sur les points de terminaison IoT Hub, consultez [Points de terminaison IoT Hub][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="39254-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="39254-140">Les didacticiels de [mise en route][lnk-get-started] vous montrent comment envoyer des messages appareil-à-cloud à partir d’appareils simulés et lire les messages à partir du point de terminaison intégré.</span><span class="sxs-lookup"><span data-stu-id="39254-140">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="39254-141">Pour plus de détails, consultez le didacticiel [Traiter les messages appareil-à-cloud IoT Hub en utilisant les itinéraires][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="39254-141">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="39254-142">Si vous voulez acheminer vos messages appareil-à-cloud vers des points de terminaison personnalisés, consultez [Utiliser des itinéraires de messages et des points de terminaison personnalisés pour les messages appareil-à-cloud][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="39254-142">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
