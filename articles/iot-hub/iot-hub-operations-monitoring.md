---
title: "Surveillance des opérations Azure IoT Hub | Microsoft Docs"
description: "Découvrez comment utiliser la surveillance des opérations Azure IoT Hub pour surveiller l’état des opérations sur votre hub IoT en temps réel."
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
ms.openlocfilehash: b6de5c5df5f9401a41be152bfa06eb994594e83d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="2bd16-103">Surveillance des opérations IoT Hub</span><span class="sxs-lookup"><span data-stu-id="2bd16-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="2bd16-104">La surveillance des opérations IoT Hub vous permet de surveiller l’état des opérations sur votre hub IoT en temps réel.</span><span class="sxs-lookup"><span data-stu-id="2bd16-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="2bd16-105">IoT Hub effectue le suivi des événements entre différentes catégories d’opérations.</span><span class="sxs-lookup"><span data-stu-id="2bd16-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="2bd16-106">Vous pouvez opter pour l’envoi des événements d’une ou plusieurs catégories à un point de terminaison de votre IoT Hub en vue de leur traitement.</span><span class="sxs-lookup"><span data-stu-id="2bd16-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="2bd16-107">Vous pouvez surveiller les données des erreurs ou configurer un traitement plus complexe basé sur des modèles de données.</span><span class="sxs-lookup"><span data-stu-id="2bd16-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="2bd16-108">IoT Hub surveille six catégories d’événements :</span><span class="sxs-lookup"><span data-stu-id="2bd16-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="2bd16-109">Opérations d’identité des appareils</span><span class="sxs-lookup"><span data-stu-id="2bd16-109">Device identity operations</span></span>
* <span data-ttu-id="2bd16-110">Télémétrie d’appareil</span><span class="sxs-lookup"><span data-stu-id="2bd16-110">Device telemetry</span></span>
* <span data-ttu-id="2bd16-111">Messages Cloud à appareil</span><span class="sxs-lookup"><span data-stu-id="2bd16-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="2bd16-112">Connexions</span><span class="sxs-lookup"><span data-stu-id="2bd16-112">Connections</span></span>
* <span data-ttu-id="2bd16-113">Chargements de fichiers</span><span class="sxs-lookup"><span data-stu-id="2bd16-113">File uploads</span></span>
* <span data-ttu-id="2bd16-114">Routage de messages</span><span class="sxs-lookup"><span data-stu-id="2bd16-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="2bd16-115">Comment activer la surveillance des opérations</span><span class="sxs-lookup"><span data-stu-id="2bd16-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="2bd16-116">Créez un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2bd16-116">Create an IoT hub.</span></span> <span data-ttu-id="2bd16-117">Pour savoir comment créer un hub IoT, consultez le guide [Prise en main][lnk-get-started].</span><span class="sxs-lookup"><span data-stu-id="2bd16-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="2bd16-118">Ouvrez le panneau de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2bd16-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="2bd16-119">De là, cliquez sur **Surveillance des opérations**.</span><span class="sxs-lookup"><span data-stu-id="2bd16-119">From there, click **Operations monitoring**.</span></span>

    ![Accéder à la configuration de la surveillance des opérations dans le portail][1]

1. <span data-ttu-id="2bd16-121">Sélectionnez les catégories de surveillance qui vous intéressent, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2bd16-121">Select the monitoring categories you wish to monitor, and then click **Save**.</span></span> <span data-ttu-id="2bd16-122">Les événements sont disponibles en lecture depuis le point de terminaison compatible avec le hub d’événements répertorié dans **Paramètres de surveillance**.</span><span class="sxs-lookup"><span data-stu-id="2bd16-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="2bd16-123">Le point de terminaison IoT Hub s’appelle `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="2bd16-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Configurer la surveillance des opérations sur votre IoT Hub][2]

> [!NOTE]
> <span data-ttu-id="2bd16-125">Si vous sélectionnez la surveillance **détaillée** dans la catégorie **Connexions**, IoT Hub génère des messages de diagnostic supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="2bd16-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="2bd16-126">Pour toutes les autres catégories, le paramètre **Détaillée** modifie la quantité d’informations qu’IoT Hub inclut dans chaque message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="2bd16-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="2bd16-127">Catégories d’événements et utilisation respective</span><span class="sxs-lookup"><span data-stu-id="2bd16-127">Event categories and how to use them</span></span>

<span data-ttu-id="2bd16-128">Chaque catégorie de surveillance d’opérations assure le suivi d’un type spécifique d’interaction avec IoT Hub et a un schéma qui définit la façon dont sont structurés les événements qu’elle comporte.</span><span class="sxs-lookup"><span data-stu-id="2bd16-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="2bd16-129">Opérations d’identité des appareils</span><span class="sxs-lookup"><span data-stu-id="2bd16-129">Device identity operations</span></span>

<span data-ttu-id="2bd16-130">La catégorie d’opérations d’identité des appareils effectue le suivi des erreurs qui se produisent quand vous tentez de créer, mettre à jour ou supprimer une entrée dans le registre d’identité de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2bd16-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="2bd16-131">Le suivi de cette catégorie est utile pour les scénarios d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="2bd16-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="2bd16-132">Télémétrie d’appareil</span><span class="sxs-lookup"><span data-stu-id="2bd16-132">Device telemetry</span></span>

<span data-ttu-id="2bd16-133">La catégorie de télémétrie d’appareil effectue le suivi des erreurs qui se produisent au niveau du hub IoT et qui sont liées au pipeline de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="2bd16-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="2bd16-134">Cette catégorie inclut notamment les erreurs concernant l’envoi d’événements de télémétrie (par exemple, une limitation) et la réception des événements de télémétrie (par exemple, un lecteur non autorisé).</span><span class="sxs-lookup"><span data-stu-id="2bd16-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="2bd16-135">Cette catégorie ne peut pas intercepter les erreurs provoquées par le code en cours d’exécution sur l’appareil lui-même.</span><span class="sxs-lookup"><span data-stu-id="2bd16-135">This category cannot catch errors caused by code running on the device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="2bd16-136">Commandes cloud-à-appareil</span><span class="sxs-lookup"><span data-stu-id="2bd16-136">Cloud-to-device commands</span></span>

<span data-ttu-id="2bd16-137">La catégorie de commandes cloud-à-appareil effectue le suivi des erreurs qui se produisent au niveau du hub IoT et qui sont liées au pipeline de messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="2bd16-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="2bd16-138">Cette catégorie inclut notamment les erreurs concernant l’envoi de messages cloud-à-appareil (telles qu’un expéditeur non autorisé), la réception des messages cloud-à-appareil (telles que le dépassement du nombre de remises) et la réception des commentaires de message cloud-à-appareil (telles que des commentaires arrivés à expiration).</span><span class="sxs-lookup"><span data-stu-id="2bd16-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="2bd16-139">Cette catégorie n’intercepte pas d’erreurs dans le cas d’un appareil qui gère mal un message cloud-à-appareil si le message a été correctement remis.</span><span class="sxs-lookup"><span data-stu-id="2bd16-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="2bd16-140">Connexions</span><span class="sxs-lookup"><span data-stu-id="2bd16-140">Connections</span></span>

<span data-ttu-id="2bd16-141">La catégorie de connexions effectue le suivi des erreurs provoquées par la connexion des appareils à un hub IoT ou leur déconnexion de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="2bd16-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="2bd16-142">Le suivi de cette catégorie est utile pour identifier les tentatives de connexion non autorisées et pour repérer les moments auxquels une connexion est perdue pour les appareils qui se trouvent dans des zones bénéficiant d’une connectivité médiocre.</span><span class="sxs-lookup"><span data-stu-id="2bd16-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="2bd16-143">Chargements de fichiers</span><span class="sxs-lookup"><span data-stu-id="2bd16-143">File uploads</span></span>

<span data-ttu-id="2bd16-144">La catégorie de chargement de fichiers effectue le suivi des erreurs qui se produisent au niveau de l’IoT hub et qui sont liées à la fonctionnalité de chargement.</span><span class="sxs-lookup"><span data-stu-id="2bd16-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="2bd16-145">Cette catégorie inclut :</span><span class="sxs-lookup"><span data-stu-id="2bd16-145">This category includes:</span></span>

* <span data-ttu-id="2bd16-146">Erreurs qui se produisent avec l’URI SAP, par exemple en cas d’expiration avant qu’un appareil notifie le hub d’un téléchargement terminé.</span><span class="sxs-lookup"><span data-stu-id="2bd16-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="2bd16-147">Échecs des téléchargements signalés par l’appareil.</span><span class="sxs-lookup"><span data-stu-id="2bd16-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="2bd16-148">Erreurs qui se produisent lorsqu’un fichier est introuvable dans le stockage lors de la création du message de notification IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2bd16-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="2bd16-149">Cette catégorie ne peut pas détecter les erreurs qui surviennent directement pendant que l’appareil charge un fichier de stockage.</span><span class="sxs-lookup"><span data-stu-id="2bd16-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="2bd16-150">Routage de messages</span><span class="sxs-lookup"><span data-stu-id="2bd16-150">Message routing</span></span>

<span data-ttu-id="2bd16-151">La catégorie de routage des messages assure le suivi des erreurs qui se produisent pendant l’évaluation du routage des messages et de l’intégrité du point de terminaison perçue par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2bd16-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="2bd16-152">Cette catégorie inclut les événements tels qu’une règle prenant la valeur « Non définie », lorsqu’IoT Hub marque un point de terminaison comme inactif et toute autre erreur reçue à partir d’un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2bd16-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="2bd16-153">Cette catégorie n’inclut pas les erreurs spécifiques sur les messages eux-mêmes (telles que les erreurs de limitation des appareils) qui sont signalées dans la catégorie « télémétrie des appareils ».</span><span class="sxs-lookup"><span data-stu-id="2bd16-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="2bd16-154">Visualiser les événements</span><span class="sxs-lookup"><span data-stu-id="2bd16-154">View events</span></span>

<span data-ttu-id="2bd16-155">Vous pouvez utiliser l’outil *iothub-explorer* pour vérifier rapidement que votre IoT Hub génère des événements de surveillance.</span><span class="sxs-lookup"><span data-stu-id="2bd16-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="2bd16-156">Pour installer l’outil, consultez les instructions dans le dépôt [iothub-explorer][lnk-iothub-explorer] GitHub.</span><span class="sxs-lookup"><span data-stu-id="2bd16-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="2bd16-157">Vérifiez que la catégorie de surveillance **Connexions** a la valeur **Verbose** (Mode détaillé) dans le portail.</span><span class="sxs-lookup"><span data-stu-id="2bd16-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="2bd16-158">À une invite de commandes, exécutez la commande suivante pour lire le point de terminaison de surveillance :</span><span class="sxs-lookup"><span data-stu-id="2bd16-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="2bd16-159">Dans une autre invite de commandes, exécutez la commande suivante pour simuler un appareil envoyant des messages de l’appareil au cloud :</span><span class="sxs-lookup"><span data-stu-id="2bd16-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="2bd16-160">La première invite de commandes affiche les événements de surveillance quand l’appareil simulé se connecte à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2bd16-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="2bd16-161">Se connecter au point de terminaison de surveillance</span><span class="sxs-lookup"><span data-stu-id="2bd16-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="2bd16-162">Le point de terminaison de surveillance de votre IoT Hub est un point de terminaison compatible Event Hub.</span><span class="sxs-lookup"><span data-stu-id="2bd16-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="2bd16-163">Vous pouvez utiliser n’importe quel mécanisme compatible avec Event Hubs pour lire les messages de surveillance à partir de ce point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2bd16-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="2bd16-164">L’exemple suivant crée un lecteur de base qui ne convient pas dans le cas d’un déploiement à débit élevé.</span><span class="sxs-lookup"><span data-stu-id="2bd16-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="2bd16-165">Pour plus d’informations sur la façon de traiter les messages à partir des concentrateurs d’événements, reportez-vous au didacticiel [Prise en main des concentrateurs d’événements][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="2bd16-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="2bd16-166">Pour vous connecter au point de terminaison de surveillance, vous avez besoin d’une chaîne de connexion et du nom du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2bd16-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="2bd16-167">Les étapes suivantes vous montrent comment trouver les valeurs nécessaires dans le portail :</span><span class="sxs-lookup"><span data-stu-id="2bd16-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="2bd16-168">Dans le portail, accédez à votre panneau de ressources IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2bd16-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="2bd16-169">Sélectionnez **Surveillance des opérations**, notez les valeurs du **Nom compatible Event Hub** et du **Point de terminaison compatible Event Hub** :</span><span class="sxs-lookup"><span data-stu-id="2bd16-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Valeurs du point de terminaison compatible Event Hub][img-endpoints]

1. <span data-ttu-id="2bd16-171">Sélectionnez **Stratégies d’accès partagé**, puis **service**.</span><span class="sxs-lookup"><span data-stu-id="2bd16-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="2bd16-172">Prenez note de la valeur de **Clé primaire** :</span><span class="sxs-lookup"><span data-stu-id="2bd16-172">Make a note of the **Primary key** value:</span></span>

    ![Clé primaire de la stratégie d’accès partagé du service][img-service-key]

<span data-ttu-id="2bd16-174">L’exemple de code C# suivant est extrait d’une application console C# **Bureau classique Windows** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2bd16-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="2bd16-175">Le projet possède le package NuGet **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="2bd16-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="2bd16-176">Remplacez l’espace réservé de chaîne de connexion par une chaîne de connexion qui utilise les valeurs du **Point de terminaison compatible Event Hub** et de la **Clé primaire** du service notées précédemment, comme l’illustre l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="2bd16-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="2bd16-177">Remplacez l’espace réservé de nom de point de terminaison de surveillance par la valeur du **Nom compatible Event Hub** notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="2bd16-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

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

## <a name="next-steps"></a><span data-ttu-id="2bd16-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2bd16-178">Next steps</span></span>
<span data-ttu-id="2bd16-179">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="2bd16-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2bd16-180">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="2bd16-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="2bd16-181">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2bd16-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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