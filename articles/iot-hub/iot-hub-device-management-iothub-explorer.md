---
title: Gestion des appareils Azure IoT avec iothub-explorer | Microsoft Docs
description: "Utilisez l’outil de ligne de commande iothub-explorer pour la gestion des appareils Azure IoT Hub, avec les méthodes directes et les options de gestion des propriétés de votre choix pour la représentation."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gestion des appareils iot azure, gestion des appareils azure iot hub, gestion des appareils iot, gestion des appareils iot hub
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: 5b7a5057bdfb5920fbb5759bed1f5561cfa1d7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="3dd0d-104">Utilisation de iothub-explorer pour la gestion des appareils Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3dd0d-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="3dd0d-106">[iothub-explorer](https://github.com/azure/iothub-explorer) est un outil en ligne de commande que vous exécutez sur un ordinateur hôte pour gérer les identités d’appareil dans votre registre de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="3dd0d-107">Il est fourni avec des options de gestion que vous pouvez utiliser pour effectuer diverses tâches.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-107">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="3dd0d-108">Option de gestion</span><span class="sxs-lookup"><span data-stu-id="3dd0d-108">Management option</span></span>          | <span data-ttu-id="3dd0d-109">Task</span><span class="sxs-lookup"><span data-stu-id="3dd0d-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3dd0d-110">Méthodes directes</span><span class="sxs-lookup"><span data-stu-id="3dd0d-110">Direct methods</span></span>             | <span data-ttu-id="3dd0d-111">Faites agir un appareil comme commençant/arrêtant d’envoyer des messages ou comme redémarrant l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-111">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="3dd0d-112">Propriétés souhaitées pour la représentation</span><span class="sxs-lookup"><span data-stu-id="3dd0d-112">Twin desired properties</span></span>    | <span data-ttu-id="3dd0d-113">Mettez un appareil dans certains états, par exemple en réglant un voyant sur le vert ou en définissant l’intervalle d’envoi de télémétrie sur 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-113">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="3dd0d-114">Propriétés signalées pour la représentation</span><span class="sxs-lookup"><span data-stu-id="3dd0d-114">Twin reported properties</span></span>   | <span data-ttu-id="3dd0d-115">Obtenez l’état signalé d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-115">Get the reported state of a device.</span></span> <span data-ttu-id="3dd0d-116">Par exemple, l’appareil signale que le voyant clignote maintenant.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-116">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="3dd0d-117">Balises de représentation</span><span class="sxs-lookup"><span data-stu-id="3dd0d-117">Twin tags</span></span>                  | <span data-ttu-id="3dd0d-118">Stocker les métadonnées spécifiques à l’appareil dans le cloud,</span><span class="sxs-lookup"><span data-stu-id="3dd0d-118">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="3dd0d-119">par exemple, l’emplacement de déploiement d’un distributeur automatique.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-119">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="3dd0d-120">Messages Cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="3dd0d-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="3dd0d-121">Envoyez des notifications à un appareil.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-121">Send notifications to a device.</span></span> <span data-ttu-id="3dd0d-122">Par exemple, « Forte probabilité de pluie aujourd'hui.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-122">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="3dd0d-123">N’oubliez pas de prendre un parapluie avec vous. »</span><span class="sxs-lookup"><span data-stu-id="3dd0d-123">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="3dd0d-124">Requêtes de représentations d’appareil</span><span class="sxs-lookup"><span data-stu-id="3dd0d-124">Device twin queries</span></span>        | <span data-ttu-id="3dd0d-125">Interrogez toutes les représentations d’appareil pour récupérer ceux avec des conditions arbitraires, comme l’identification des appareils qui sont disponibles pour utilisation.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-125">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="3dd0d-126">Pour plus d’explications sur les différences et des conseils sur l’utilisation de ces options, consultez [l’aide sur la communication appareil-à-cloud](iot-hub-devguide-d2c-guidance.md) et [l’aide sur la communication cloud-à-appareil](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="3dd0d-126">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3dd0d-127">Les représentations d’appareil sont des documents JSON qui stockent des informations sur l’état des appareils (métadonnées, configurations et conditions).</span><span class="sxs-lookup"><span data-stu-id="3dd0d-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="3dd0d-128">IoT Hub conserve une représentation d’appareil pour chaque appareil que vous y connectez.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-128">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="3dd0d-129">Pour plus d’informations sur les représentations d’appareil, consultez [Prise en main des représentations d’appareils](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="3dd0d-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3dd0d-130">Contenu</span><span class="sxs-lookup"><span data-stu-id="3dd0d-130">What you learn</span></span>

<span data-ttu-id="3dd0d-131">Vous allez apprendre à utiliser iothub-explorer avec diverses options de gestion sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3dd0d-132">Procédure</span><span class="sxs-lookup"><span data-stu-id="3dd0d-132">What you do</span></span>

<span data-ttu-id="3dd0d-133">Exécutez iothub-diverses avec diverses options de gestion.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3dd0d-134">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="3dd0d-134">What you need</span></span>

- <span data-ttu-id="3dd0d-135">Le didacticiel [Configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé, qui traite des exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="3dd0d-136">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="3dd0d-137">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="3dd0d-138">Une application cliente qui envoie des messages à votre instance Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-138">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="3dd0d-139">Vérifiez que votre appareil exécute l’application cliente tout au long de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-139">Make sure your device is running with the client application during this tutorial.</span></span>
- <span data-ttu-id="3dd0d-140">iothub-explorer, [Installez iothub-explorer](https://github.com/azure/iothub-explorer) sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="3dd0d-141">Connexion à votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3dd0d-141">Connect to your IoT hub</span></span>

<span data-ttu-id="3dd0d-142">Connectez-vous à votre IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-142">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="3dd0d-143">Utilisation d’iothub-explorer avec des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="3dd0d-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="3dd0d-144">Appelez la méthode `start` dans l’application de l’appareil pour envoyer des messages à votre IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-144">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="3dd0d-145">Appelez la méthode `stop` dans l’application de l’appareil pour arrêter d’envoyer des messages à votre IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-145">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="3dd0d-146">Utiliser iothub-explorer avec les propriétés de représentation souhaitées</span><span class="sxs-lookup"><span data-stu-id="3dd0d-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="3dd0d-147">Définissez un intervalle de propriété = 3000 en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-147">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="3dd0d-148">Cette propriété peut être lue par votre appareil.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="3dd0d-149">Utiliser iothub-explorer avec les propriétés signalées pour la représentation</span><span class="sxs-lookup"><span data-stu-id="3dd0d-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="3dd0d-150">Obtenez les propriétés signalées de l’appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-150">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="3dd0d-151">Une des propriétés est $metadata.$lastUpdated qui indique la dernière fois que cet appareil a envoyé ou reçu un message.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-151">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="3dd0d-152">Utilisez iothub-explorer avec les balises de représentation</span><span class="sxs-lookup"><span data-stu-id="3dd0d-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="3dd0d-153">Affichez les balises et les propriétés de votre appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-153">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="3dd0d-154">Ajoutez un champ role = temperature&humidity à l’appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-154">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="3dd0d-155">Utiliser iothub-explorer avec les messages cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="3dd0d-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="3dd0d-156">Envoyez un message « Hello World » à l’appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-156">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="3dd0d-157">Consultez [Utiliser Iothub-explorer pour envoyer et recevoir des messages entre votre appareil et IoT Hub](iot-hub-explorer-cloud-device-messaging.md) pour un scénario réel d’utilisation de cette commande.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-157">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="3dd0d-158">Utiliser iothub-explorer avec des requêtes de représentation d’appareil</span><span class="sxs-lookup"><span data-stu-id="3dd0d-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="3dd0d-159">Interrogez les appareils avec une balise role = temperature&humidity en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-159">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="3dd0d-160">Interrogez les appareils, à l’exception de ceux qui ont une balise role = temperature&humidity en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd0d-160">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="3dd0d-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3dd0d-161">Next steps</span></span>

<span data-ttu-id="3dd0d-162">Vous avez appris à utiliser iothub-explorer avec diverses options de gestion.</span><span class="sxs-lookup"><span data-stu-id="3dd0d-162">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
