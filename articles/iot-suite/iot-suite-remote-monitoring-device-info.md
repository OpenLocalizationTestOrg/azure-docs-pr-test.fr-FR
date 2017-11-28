---
title: "Métadonnées d’informations sur l’appareil dans la solution de surveillance à distance | Microsoft Docs"
description: "Description de la solution préconfigurée de surveillance à distance Azure IoT et de son architecture"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: f8fd452806a0a0b98cf8e434c9bd55700083a6c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="device-information-metadata-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="09ee7-103">Métadonnées relatives aux informations d’appareil dans la solution préconfigurée de surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="09ee7-103">Device information metadata in the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="09ee7-104">La solution préconfigurée de surveillance à distance Azure IoT Suite montre une approche de gestion des métadonnées d’appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="09ee7-105">Cet article décrit l’approche de cette solution pour vous permettre de comprendre :</span><span class="sxs-lookup"><span data-stu-id="09ee7-105">This article outlines the approach this solution takes to enable you to understand:</span></span>

* <span data-ttu-id="09ee7-106">Quelles métadonnées d’appareil sont stockées par la solution.</span><span class="sxs-lookup"><span data-stu-id="09ee7-106">What device metadata the solution stores.</span></span>
* <span data-ttu-id="09ee7-107">Comment la solution gère les métadonnées d’appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-107">How the solution manages the device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="09ee7-108">Context</span><span class="sxs-lookup"><span data-stu-id="09ee7-108">Context</span></span>

<span data-ttu-id="09ee7-109">La solution préconfigurée de surveillance à distance utilise [Azure IoT Hub][lnk-iot-hub] pour permettre à vos appareils d’envoyer des données vers le cloud.</span><span class="sxs-lookup"><span data-stu-id="09ee7-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span></span> <span data-ttu-id="09ee7-110">La solution stocke des informations sur les appareils dans trois emplacements différents :</span><span class="sxs-lookup"><span data-stu-id="09ee7-110">The solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="09ee7-111">Emplacement</span><span class="sxs-lookup"><span data-stu-id="09ee7-111">Location</span></span> | <span data-ttu-id="09ee7-112">Informations stockées</span><span class="sxs-lookup"><span data-stu-id="09ee7-112">Information stored</span></span> | <span data-ttu-id="09ee7-113">Implémentation</span><span class="sxs-lookup"><span data-stu-id="09ee7-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="09ee7-114">Registre des identités</span><span class="sxs-lookup"><span data-stu-id="09ee7-114">Identity registry</span></span> | <span data-ttu-id="09ee7-115">ID de l’appareil, clés d’authentification, état Activé</span><span class="sxs-lookup"><span data-stu-id="09ee7-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="09ee7-116">Intégré à IoT Hub</span><span class="sxs-lookup"><span data-stu-id="09ee7-116">Built in to IoT Hub</span></span> |
| <span data-ttu-id="09ee7-117">Représentations d’appareil physique</span><span class="sxs-lookup"><span data-stu-id="09ee7-117">Device twins</span></span> | <span data-ttu-id="09ee7-118">Métadonnées : propriétés signalées, propriétés souhaitées, balises</span><span class="sxs-lookup"><span data-stu-id="09ee7-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="09ee7-119">Intégré à IoT Hub</span><span class="sxs-lookup"><span data-stu-id="09ee7-119">Built in to IoT Hub</span></span> |
| <span data-ttu-id="09ee7-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="09ee7-120">Cosmos DB</span></span> | <span data-ttu-id="09ee7-121">Historique des commandes et méthodes</span><span class="sxs-lookup"><span data-stu-id="09ee7-121">Command and method history</span></span> | <span data-ttu-id="09ee7-122">Personnalisé pour la solution</span><span class="sxs-lookup"><span data-stu-id="09ee7-122">Custom for solution</span></span> |

<span data-ttu-id="09ee7-123">IoT Hub inclut un [registre des identités des appareils][lnk-identity-registry] pour gérer l’accès à un IoT Hub et utilise des [jumeaux d’appareil][lnk-device-twin] pour gérer les métadonnées de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span></span> <span data-ttu-id="09ee7-124">Il inclut également un *registre des appareils* spécifique à la solution de surveillance à distance qui stocke l’historique des commandes et méthodes.</span><span class="sxs-lookup"><span data-stu-id="09ee7-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="09ee7-125">La solution de surveillance à distance utilise une base de données [Cosmos DB][lnk-docdb] afin d’implémenter un magasin personnalisé pour l’historique des commandes et méthodes.</span><span class="sxs-lookup"><span data-stu-id="09ee7-125">The remote monitoring solution uses a [Cosmos DB][lnk-docdb] database to implement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="09ee7-126">La solution préconfigurée de surveillance à distance synchronise le registre des identités des appareils avec les informations de la base de données Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="09ee7-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the Cosmos DB database.</span></span> <span data-ttu-id="09ee7-127">Les deux utilisent le même id d’appareil pour identifier chaque appareil connecté à votre IoT hub de manière unique.</span><span class="sxs-lookup"><span data-stu-id="09ee7-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="09ee7-128">Métadonnées de l’appareil</span><span class="sxs-lookup"><span data-stu-id="09ee7-128">Device metadata</span></span>

<span data-ttu-id="09ee7-129">IoT Hub gère un [jumeau d’appareil][lnk-device-twin] pour chaque appareil simulé et physique connecté à une solution de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="09ee7-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span></span> <span data-ttu-id="09ee7-130">La solution utilise des jumeaux d’appareil pour gérer les métadonnées associées aux appareils.</span><span class="sxs-lookup"><span data-stu-id="09ee7-130">The solution uses device twins to manage the metadata associated with devices.</span></span> <span data-ttu-id="09ee7-131">Un jumeau d’appareil est un document JSON géré par IoT Hub et la solution utilise l’API IoT Hub pour interagir avec les jumeaux d’appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span></span>

<span data-ttu-id="09ee7-132">Un jumeau d’appareil stocke trois types de métadonnées :</span><span class="sxs-lookup"><span data-stu-id="09ee7-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="09ee7-133">Les *propriétés signalées* sont envoyées à un IoT Hub par un appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-133">*Reported properties* are sent to an IoT hub by a device.</span></span> <span data-ttu-id="09ee7-134">Dans la solution de surveillance à distance, les appareils simulés envoient les propriétés signalées au démarrage et en réponse aux commandes et méthodes **Modifier l’état de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="09ee7-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span></span> <span data-ttu-id="09ee7-135">Vous pouvez afficher les propriétés signalées dans la **liste des appareils** et les **informations sur l’appareil** dans le portail de solution.</span><span class="sxs-lookup"><span data-stu-id="09ee7-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span></span> <span data-ttu-id="09ee7-136">Les propriétés signalées sont en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="09ee7-136">Reported properties are read only.</span></span>
- <span data-ttu-id="09ee7-137">Les *propriétés souhaitées* sont récupérées à partir d’IoT Hub IoT par les appareils.</span><span class="sxs-lookup"><span data-stu-id="09ee7-137">*Desired properties* are retrieved from the IoT hub by devices.</span></span> <span data-ttu-id="09ee7-138">C’est l’appareil qui doit effectuer les modifications de configuration nécessaires sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-138">It is the responsibility of the device to make any necessary configuration change on the device.</span></span> <span data-ttu-id="09ee7-139">C’est également l’appareil qui doit signaler la modification au hub sous la forme d’une propriété signalée.</span><span class="sxs-lookup"><span data-stu-id="09ee7-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span></span> <span data-ttu-id="09ee7-140">Vous pouvez définir une valeur de propriété souhaitée via le portail de solution.</span><span class="sxs-lookup"><span data-stu-id="09ee7-140">You can set a desired property value through the solution portal.</span></span>
- <span data-ttu-id="09ee7-141">Les *balises* existent seulement dans le jumeau d’appareil et ne sont jamais synchronisés avec un appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-141">*Tags* only exist in the device twin and are never synchronized with a device.</span></span> <span data-ttu-id="09ee7-142">Vous pouvez définir des valeurs de balise dans le portail de solution et les utiliser lorsque vous filtrez la liste des appareils.</span><span class="sxs-lookup"><span data-stu-id="09ee7-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span></span> <span data-ttu-id="09ee7-143">La solution utilise également une balise pour identifier l’icône à afficher pour un appareil dans le portail de solution.</span><span class="sxs-lookup"><span data-stu-id="09ee7-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span></span>

<span data-ttu-id="09ee7-144">Les propriétés signalées à partir des appareils simulés sont par exemple le fabricant, le numéro de modèle, la latitude et la longitude.</span><span class="sxs-lookup"><span data-stu-id="09ee7-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="09ee7-145">Les appareils simulés retournent également la liste des méthodes prises en charge sous la forme d’une propriété signalée.</span><span class="sxs-lookup"><span data-stu-id="09ee7-145">Simulated devices also return the list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="09ee7-146">Le code d’appareil simulé utilise uniquement les propriétés souhaitées **Desired.Config.TemperatureMeanValue** et **Desired.Config.TelemetryInterval** pour mettre à jour les propriétés signalées renvoyées à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09ee7-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="09ee7-147">Toutes les autres demandes de modification de propriétés souhaitées sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="09ee7-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="09ee7-148">Un document JSON des métadonnées relatives aux informations d’appareil stocké dans la base de données Cosmos DB du registre des appareils présente la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="09ee7-148">A device information metadata JSON document stored in the device registry Cosmos DB database has the following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="09ee7-149">Les informations d’appareil peuvent également inclure des métadonnées permettant de décrire la télémétrie que l’appareil envoie au IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09ee7-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span></span> <span data-ttu-id="09ee7-150">La solution de surveillance à distance utilise ces métadonnées de télémétrie pour personnaliser la façon dont le tableau de bord affiche la [télémétrie dynamique][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="09ee7-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="09ee7-151">Cycle de vie</span><span class="sxs-lookup"><span data-stu-id="09ee7-151">Lifecycle</span></span>

<span data-ttu-id="09ee7-152">Lorsque vous créez un appareil dans le portail de solution, la solution crée une entrée dans la base de données Cosmos DB pour stocker l’historique des commandes et méthodes.</span><span class="sxs-lookup"><span data-stu-id="09ee7-152">When you first create a device in the solution portal, the solution creates an entry in the Cosmos DB database to store command and method history.</span></span> <span data-ttu-id="09ee7-153">À ce stade, la solution crée également une entrée pour l’appareil dans le registre des identités des appareils, qui génère les clés utilisées par l’appareil pour s’authentifier avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09ee7-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span></span> <span data-ttu-id="09ee7-154">Elle crée également un jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-154">It also creates a device twin.</span></span>

<span data-ttu-id="09ee7-155">Lorsqu’un appareil se connecte pour la première fois à la solution, il envoie les propriétés signalées et un message d’informations sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-155">When a device first connects to the solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="09ee7-156">Les valeurs des propriétés signalées sont automatiquement enregistrées dans le jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-156">The reported property values are automatically saved in the device twin.</span></span> <span data-ttu-id="09ee7-157">Les propriétés signalées incluent le fabricant de l’appareil, le numéro du modèle, le numéro de série et une liste des méthodes prises en charge.</span><span class="sxs-lookup"><span data-stu-id="09ee7-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="09ee7-158">Un message d’informations sur l’appareil inclut la liste des commandes prises en charge par l’appareil comprenant des informations sur les paramètres de commande.</span><span class="sxs-lookup"><span data-stu-id="09ee7-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span></span> <span data-ttu-id="09ee7-159">Lorsque la solution reçoit ce message, elle met à jour les informations de l’appareil dans la base de données Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="09ee7-159">When the solution receives this message, it updates the device information in the Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-the-solution-portal"></a><span data-ttu-id="09ee7-160">Afficher et modifier les informations d’appareil dans le portail de la solution</span><span class="sxs-lookup"><span data-stu-id="09ee7-160">View and edit device information in the solution portal</span></span>

<span data-ttu-id="09ee7-161">La liste des appareils du portail de solution affiche par défaut les propriétés d’appareil suivantes sous forme de colonnes : **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor** et **Installed RAM**.</span><span class="sxs-lookup"><span data-stu-id="09ee7-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="09ee7-162">Vous pouvez personnaliser les colonnes en cliquant sur **l’éditeur de colonne**.</span><span class="sxs-lookup"><span data-stu-id="09ee7-162">You can customize the columns by clicking **Column editor**.</span></span> <span data-ttu-id="09ee7-163">Les propriétés d’appareil **Latitude** et **Longitude** indiquent l’emplacement dans la Carte Bing sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="09ee7-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span></span>

![Éditeur de colonne dans la liste des appareils][img-device-list]

<span data-ttu-id="09ee7-165">Dans le volet **Informations sur l’appareil** du portail de solution, vous pouvez modifier les balises et les propriétés souhaitées (les propriétés signalées sont en lecture seule).</span><span class="sxs-lookup"><span data-stu-id="09ee7-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Volet d’informations sur l’appareil][img-device-edit]

<span data-ttu-id="09ee7-167">Vous pouvez utiliser le portail de la solution pour supprimer un appareil de votre solution.</span><span class="sxs-lookup"><span data-stu-id="09ee7-167">You can use the solution portal to remove a device from your solution.</span></span> <span data-ttu-id="09ee7-168">Lorsque vous supprimez un appareil, la solution supprime l’entrée de l’appareil du registre d’identité, puis supprime le jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="09ee7-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span></span> <span data-ttu-id="09ee7-169">La solution supprime également les informations relatives à l’appareil de la base de données Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="09ee7-169">The solution also removes information related to the device from the Cosmos DB database.</span></span> <span data-ttu-id="09ee7-170">Avant de pouvoir supprimer un appareil, vous devez le désactiver.</span><span class="sxs-lookup"><span data-stu-id="09ee7-170">Before you can remove a device, you must disable it.</span></span>

![Supprimer l’appareil][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="09ee7-172">Traitement des messages d’information d’appareil</span><span class="sxs-lookup"><span data-stu-id="09ee7-172">Device information message processing</span></span>

<span data-ttu-id="09ee7-173">Les messages d’information d’appareil envoyés par un appareil sont différents des messages de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="09ee7-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="09ee7-174">Les messages d’information sur l’appareil incluent les commandes auxquelles répond un appareil et l’historique des commandes.</span><span class="sxs-lookup"><span data-stu-id="09ee7-174">Device information messages include the commands a device can respond to, and any command history.</span></span> <span data-ttu-id="09ee7-175">IoT Hub lui-même n’a aucune connaissance des métadonnées contenues dans un message d’information d’appareil et traite le message de la même manière qu’il traite tout message appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="09ee7-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="09ee7-176">Dans la solution de surveillance à distance, une tâche [Azure Stream Analytics][lnk-stream-analytics] (ASA) lit les messages issus de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09ee7-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span></span> <span data-ttu-id="09ee7-177">Le travail **DeviceInfo** Stream Analytics filtre les messages contenant **« ObjectType » : « DeviceInfo »** et les transmet à l’instance hôte **EventProcessorHost** qui s’exécute dans une tâche web.</span><span class="sxs-lookup"><span data-stu-id="09ee7-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="09ee7-178">La logique de l’instance **EventProcessorHost** utilise l’ID d’appareil pour rechercher l’enregistrement Cosmos DB de l’appareil spécifique et le mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="09ee7-178">Logic in the **EventProcessorHost** instance uses the device id to find the Cosmos DB record for the specific device and update the record.</span></span>

> [!NOTE]
> <span data-ttu-id="09ee7-179">Un message d’information d’appareil est un message appareil-à-cloud standard.</span><span class="sxs-lookup"><span data-stu-id="09ee7-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="09ee7-180">La solution fait la distinction entre les messages d’information d’appareil et les messages de télémétrie en utilisant des requêtes ASA.</span><span class="sxs-lookup"><span data-stu-id="09ee7-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09ee7-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09ee7-181">Next steps</span></span>

<span data-ttu-id="09ee7-182">Maintenant que vous savez comment personnaliser les solutions préconfigurées, vous pouvez explorer certaines des autres fonctions et fonctionnalités des solutions préconfigurées de la suite IoT :</span><span class="sxs-lookup"><span data-stu-id="09ee7-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="09ee7-183">[Présentation de la solution préconfigurée de maintenance prédictive][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="09ee7-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="09ee7-184">[Forum Aux Questions (FAQ) relatives à IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="09ee7-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="09ee7-185">[Sécurisation de l’Internet des objets de bout en bout][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="09ee7-185">[IoT security from the ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
