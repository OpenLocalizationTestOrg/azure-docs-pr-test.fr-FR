---
title: "surveillance des opérations IoT Hub aaaAzure | Documents Microsoft"
description: "Comment les opérations de Azure IoT Hub toouse analyse toomonitor hello état des opérations sur votre IoT hub en temps réel."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="b77e8-103">Surveillance des opérations IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b77e8-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="b77e8-104">Surveillance des opérations IoT Hub vous permet d’état de hello toomonitor des opérations sur votre IoT hub en temps réel.</span><span class="sxs-lookup"><span data-stu-id="b77e8-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="b77e8-105">IoT Hub effectue le suivi des événements entre différentes catégories d’opérations.</span><span class="sxs-lookup"><span data-stu-id="b77e8-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="b77e8-106">Vous pouvez choisir d’envoyer des événements à partir d’une ou plusieurs catégories tooan point de terminaison de votre hub IoT pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="b77e8-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="b77e8-107">Vous pouvez analyser les données hello pour les erreurs ou configurer un traitement plus complexe basé sur des modèles de données.</span><span class="sxs-lookup"><span data-stu-id="b77e8-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="b77e8-108">IoT Hub surveille six catégories d’événements :</span><span class="sxs-lookup"><span data-stu-id="b77e8-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="b77e8-109">Opérations d’identité des appareils</span><span class="sxs-lookup"><span data-stu-id="b77e8-109">Device identity operations</span></span>
* <span data-ttu-id="b77e8-110">Télémétrie d’appareil</span><span class="sxs-lookup"><span data-stu-id="b77e8-110">Device telemetry</span></span>
* <span data-ttu-id="b77e8-111">Messages Cloud à appareil</span><span class="sxs-lookup"><span data-stu-id="b77e8-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="b77e8-112">Connexions</span><span class="sxs-lookup"><span data-stu-id="b77e8-112">Connections</span></span>
* <span data-ttu-id="b77e8-113">Chargements de fichiers</span><span class="sxs-lookup"><span data-stu-id="b77e8-113">File uploads</span></span>
* <span data-ttu-id="b77e8-114">Routage de messages</span><span class="sxs-lookup"><span data-stu-id="b77e8-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="b77e8-115">La surveillance des opérations tooenable</span><span class="sxs-lookup"><span data-stu-id="b77e8-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="b77e8-116">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b77e8-116">Create an IoT hub.</span></span> <span data-ttu-id="b77e8-117">Vous trouverez des instructions sur la façon de toocreate un hub IoT Bonjour [prise en main] [ lnk-get-started] guide.</span><span class="sxs-lookup"><span data-stu-id="b77e8-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="b77e8-118">Ouvrez le panneau hello de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b77e8-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="b77e8-119">De là, cliquez sur **Surveillance des opérations**.</span><span class="sxs-lookup"><span data-stu-id="b77e8-119">From there, click **Operations monitoring**.</span></span>

    ![Opérations d’accès hello portail d’analyse][1]

1. <span data-ttu-id="b77e8-121">Hello Sélectionnez analyse des catégories que vous souhaitez toomonitor, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b77e8-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="b77e8-122">Hello événements sont disponibles pour la lecture à partir du point de terminaison hello compatible concentrateur d’événements répertoriée dans **paramètres d’analyse**.</span><span class="sxs-lookup"><span data-stu-id="b77e8-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="b77e8-123">Hello point de terminaison IoT Hub est appelée `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="b77e8-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Configurer la surveillance des opérations sur votre IoT Hub][2]

> [!NOTE]
> <span data-ttu-id="b77e8-125">En sélectionnant **Verbose** analyse pour hello **connexions** catégorie provoque IoT Hub toogenerate les messages de diagnostic supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b77e8-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="b77e8-126">Pour toutes les autres catégories, hello **Verbose** inclut les modifications apportées au paramètre quantité hello d’informations IoT Hub dans chaque message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="b77e8-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="b77e8-127">Catégories d’événements et comment toouse les</span><span class="sxs-lookup"><span data-stu-id="b77e8-127">Event categories and how toouse them</span></span>

<span data-ttu-id="b77e8-128">Chaque catégorie de surveillance d’opérations assure le suivi d’un type spécifique d’interaction avec IoT Hub et a un schéma qui définit la façon dont sont structurés les événements qu’elle comporte.</span><span class="sxs-lookup"><span data-stu-id="b77e8-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="b77e8-129">Opérations d’identité des appareils</span><span class="sxs-lookup"><span data-stu-id="b77e8-129">Device identity operations</span></span>

<span data-ttu-id="b77e8-130">catégorie d’opérations Hello appareils identité effectue le suivi des erreurs qui se produisent lorsque vous essayez de toocreate, mettre à jour ou supprimer une entrée dans le Registre des identités de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b77e8-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="b77e8-131">Le suivi de cette catégorie est utile pour les scénarios d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="b77e8-131">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a><span data-ttu-id="b77e8-132">Télémétrie d’appareil</span><span class="sxs-lookup"><span data-stu-id="b77e8-132">Device telemetry</span></span>

<span data-ttu-id="b77e8-133">catégorie de télémétrie de périphérique Hello effectue le suivi des erreurs qui se produisent au hub IoT de hello et sont le pipeline de télémétrie toohello connexes.</span><span class="sxs-lookup"><span data-stu-id="b77e8-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="b77e8-134">Cette catégorie inclut notamment les erreurs concernant l’envoi d’événements de télémétrie (par exemple, une limitation) et la réception des événements de télémétrie (par exemple, un lecteur non autorisé).</span><span class="sxs-lookup"><span data-stu-id="b77e8-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="b77e8-135">Cette catégorie ne peut pas intercepter des erreurs provoquées par le code en cours d’exécution sur l’appareil hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="b77e8-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a><span data-ttu-id="b77e8-136">Commandes cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="b77e8-136">Cloud-to-device commands</span></span>

<span data-ttu-id="b77e8-137">catégorie de commandes de cloud-à-appareil Hello effectue le suivi des erreurs qui se produisent au hub IoT de hello et sont le pipeline de message du cloud-à-appareil toohello connexes.</span><span class="sxs-lookup"><span data-stu-id="b77e8-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="b77e8-138">Cette catégorie inclut notamment les erreurs concernant l’envoi de messages cloud-à-appareil (telles qu’un expéditeur non autorisé), la réception des messages cloud-à-appareil (telles que le dépassement du nombre de remises) et la réception des commentaires de message cloud-à-appareil (telles que des commentaires arrivés à expiration).</span><span class="sxs-lookup"><span data-stu-id="b77e8-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="b77e8-139">Cette catégorie n’intercepte pas d’erreurs à partir d’un périphérique qui gère correctement un message cloud-à-appareil si le message de salutation cloud sur l’appareil a été remis avec succès.</span><span class="sxs-lookup"><span data-stu-id="b77e8-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a><span data-ttu-id="b77e8-140">Connexions</span><span class="sxs-lookup"><span data-stu-id="b77e8-140">Connections</span></span>

<span data-ttu-id="b77e8-141">catégorie de connexions Hello effectue le suivi des erreurs qui se produisent lorsque les appareils se connecteront ou se déconnecter d’un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b77e8-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="b77e8-142">Le suivi de cette catégorie est utile pour identifier les tentatives de connexion non autorisées et pour repérer les moments auxquels une connexion est perdue pour les appareils qui se trouvent dans des zones bénéficiant d’une connectivité médiocre.</span><span class="sxs-lookup"><span data-stu-id="b77e8-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a><span data-ttu-id="b77e8-143">Chargements de fichiers</span><span class="sxs-lookup"><span data-stu-id="b77e8-143">File uploads</span></span>

<span data-ttu-id="b77e8-144">catégorie de téléchargement de fichier Hello effectue le suivi des erreurs qui se produisent au hub IoT de hello et sont une fonctionnalité de téléchargement toofile connexes.</span><span class="sxs-lookup"><span data-stu-id="b77e8-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="b77e8-145">Cette catégorie inclut :</span><span class="sxs-lookup"><span data-stu-id="b77e8-145">This category includes:</span></span>

* <span data-ttu-id="b77e8-146">Erreurs qui se produisent avec hello SAS URI, par exemple lorsqu’il expire avant un périphérique notifie hub hello d’un téléchargement terminé.</span><span class="sxs-lookup"><span data-stu-id="b77e8-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="b77e8-147">Échec de téléchargements signalées par le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="b77e8-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="b77e8-148">Erreurs qui se produisent lorsqu’un fichier est introuvable dans le stockage lors de la création du message de notification IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b77e8-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="b77e8-149">Cette catégorie ne peut pas intercepter les erreurs qui directement se produisent lors de l’appareil de hello transfère un toostorage de fichier.</span><span class="sxs-lookup"><span data-stu-id="b77e8-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a><span data-ttu-id="b77e8-150">Routage de messages</span><span class="sxs-lookup"><span data-stu-id="b77e8-150">Message routing</span></span>

<span data-ttu-id="b77e8-151">catégorie du routage des messages Hello effectue le suivi des erreurs qui se produisent pendant l’évaluation de routage de message et de contrôle d’intégrité du point de terminaison perçue par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b77e8-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="b77e8-152">Cette catégorie inclut des événements tels que lorsqu’une règle prend trop « indéfini », lorsque IoT Hub la marque un point de terminaison en tant que de lettres mortes et les autres erreurs reçues à partir d’un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="b77e8-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="b77e8-153">Cette catégorie n’inclut pas les erreurs spécifiques sur les messages hello eux-mêmes (par exemple, le périphérique erreurs de limitation), qui sont signalées sous la catégorie de « télémétrie de l’appareil » hello.</span><span class="sxs-lookup"><span data-stu-id="b77e8-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a><span data-ttu-id="b77e8-154">Visualiser les événements</span><span class="sxs-lookup"><span data-stu-id="b77e8-154">View events</span></span>

<span data-ttu-id="b77e8-155">Vous pouvez utiliser hello *iothub-explorer* tooquickly de l’outil de test que votre hub IoT génère des événements de contrôle.</span><span class="sxs-lookup"><span data-stu-id="b77e8-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="b77e8-156">tooinstall hello outil, consultez les instructions hello Bonjour [iothub-explorer] [ lnk-iothub-explorer] référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="b77e8-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="b77e8-157">Vérifiez que hello **connexions** analyse catégorie est défini trop**Verbose** dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="b77e8-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="b77e8-158">À une invite de commandes, exécutez hello suivant commande tooread hello surveillance de point de terminaison :</span><span class="sxs-lookup"><span data-stu-id="b77e8-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="b77e8-159">Dans l’invite de commandes une autre, exécutez hello suivant commande toosimulate un périphérique d’envoi de messages de l’appareil-à-cloud :</span><span class="sxs-lookup"><span data-stu-id="b77e8-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="b77e8-160">Hello première ligne de commande affiche les événements de surveillance de hello comme tooyour IoT hub connecte l’appareil simulé de hello.</span><span class="sxs-lookup"><span data-stu-id="b77e8-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="b77e8-161">Se connecter toohello surveillance de point de terminaison</span><span class="sxs-lookup"><span data-stu-id="b77e8-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="b77e8-162">Hello surveillance de point de terminaison sur votre hub IoT est un point de terminaison de Hub d’événements compatibles.</span><span class="sxs-lookup"><span data-stu-id="b77e8-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="b77e8-163">Vous pouvez utiliser n’importe quel mécanisme qui fonctionne avec les concentrateurs d’événements tooread analyse les messages à partir de ce point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="b77e8-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="b77e8-164">Hello exemple suivant crée un lecteur de base qui n’est pas approprié pour un déploiement d’un débit élevé.</span><span class="sxs-lookup"><span data-stu-id="b77e8-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="b77e8-165">Pour plus d’informations sur la tooprocess des messages à partir de concentrateurs d’événements, consultez hello [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b77e8-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="b77e8-166">point de terminaison analyse tooconnect toohello, vous devez un nom de point de terminaison hello et de chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="b77e8-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="b77e8-167">Hello suit vous montrent comment toofind hello les valeurs nécessaires dans le portail de hello :</span><span class="sxs-lookup"><span data-stu-id="b77e8-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="b77e8-168">Dans le portail de hello, accédez tooyour panneau des ressources IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b77e8-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="b77e8-169">Choisissez **surveillance des opérations**et prenez note de hello **nom du concentrateur d’événements compatibles** et **point de terminaison de Hub d’événements compatibles** valeurs :</span><span class="sxs-lookup"><span data-stu-id="b77e8-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Valeurs du point de terminaison compatible Event Hub][img-endpoints]

1. <span data-ttu-id="b77e8-171">Sélectionnez **Stratégies d’accès partagé**, puis **service**.</span><span class="sxs-lookup"><span data-stu-id="b77e8-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="b77e8-172">Prenez note de hello **clé primaire** valeur :</span><span class="sxs-lookup"><span data-stu-id="b77e8-172">Make a note of hello **Primary key** value:</span></span>

    ![Clé primaire de la stratégie d’accès partagé du service][img-service-key]

<span data-ttu-id="b77e8-174">exemple de code c# suivant Hello est effectuée à partir de Visual Studio **de bureau Windows classique** application de console c#.</span><span class="sxs-lookup"><span data-stu-id="b77e8-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="b77e8-175">projet de Hello a hello **WindowsAzure.ServiceBus** package NuGet installé.</span><span class="sxs-lookup"><span data-stu-id="b77e8-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="b77e8-176">Remplacez l’espace réservé chaîne de connexion hello avec une chaîne de connexion qui utilise hello **point de terminaison de Hub d’événements compatibles** et le service **clé primaire** valeurs notées précédemment, comme indiqué dans les éléments suivants de hello exemple :</span><span class="sxs-lookup"><span data-stu-id="b77e8-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="b77e8-177">Remplacez hello analyse l’espace réservé de nom de point de terminaison avec hello **nom du concentrateur d’événements compatibles** valeur que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="b77e8-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b77e8-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b77e8-178">Next steps</span></span>
<span data-ttu-id="b77e8-179">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="b77e8-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b77e8-180">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="b77e8-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="b77e8-181">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b77e8-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md