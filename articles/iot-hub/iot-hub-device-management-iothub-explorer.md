---
title: aaaAzure gestion des appareils IoT avec iothub-explorer | Documents Microsoft
description: "Utilisez hello iothub-CLI outil Explorateur pour la gestion des appareils Azure IoT Hub, présentant les méthodes directes hello et options de gestion de propriétés souhaitées du double hello."
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
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="9be1c-104">Utilisation de iothub-explorer pour la gestion des appareils Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9be1c-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="9be1c-106">[Explorateur d’iothub](https://github.com/azure/iothub-explorer) est un outil d’interface CLI que vous exécutez sur une identité d’appareil hôte ordinateur toomanage dans le Registre du hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9be1c-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="9be1c-107">Il est fourni avec les options de gestion que vous pouvez utiliser tooperform différentes tâches.</span><span class="sxs-lookup"><span data-stu-id="9be1c-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="9be1c-108">Option de gestion</span><span class="sxs-lookup"><span data-stu-id="9be1c-108">Management option</span></span>          | <span data-ttu-id="9be1c-109">Task</span><span class="sxs-lookup"><span data-stu-id="9be1c-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9be1c-110">Méthodes directes</span><span class="sxs-lookup"><span data-stu-id="9be1c-110">Direct methods</span></span>             | <span data-ttu-id="9be1c-111">Rendre un périphérique agissent comme le démarrage ou l’arrêt d’envoi de messages ou le redémarrage du périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="9be1c-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="9be1c-112">Propriétés souhaitées pour la représentation</span><span class="sxs-lookup"><span data-stu-id="9be1c-112">Twin desired properties</span></span>    | <span data-ttu-id="9be1c-113">Mettre un appareil dans certains États, telles que la définition d’un toogreen LED ou définition de données de télémétrie hello too30 intervalle d’envoi.</span><span class="sxs-lookup"><span data-stu-id="9be1c-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="9be1c-114">Propriétés signalées pour la représentation</span><span class="sxs-lookup"><span data-stu-id="9be1c-114">Twin reported properties</span></span>   | <span data-ttu-id="9be1c-115">Obtenir hello a signalé l’état d’un périphérique.</span><span class="sxs-lookup"><span data-stu-id="9be1c-115">Get hello reported state of a device.</span></span> <span data-ttu-id="9be1c-116">Par exemple, les appareils hello signale hello que LED clignote maintenant.</span><span class="sxs-lookup"><span data-stu-id="9be1c-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="9be1c-117">Balises de représentation</span><span class="sxs-lookup"><span data-stu-id="9be1c-117">Twin tags</span></span>                  | <span data-ttu-id="9be1c-118">Stocker les métadonnées spécifiques au périphérique dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="9be1c-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="9be1c-119">Par exemple, hello emplacement de déploiement d’un distributeur automatique.</span><span class="sxs-lookup"><span data-stu-id="9be1c-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="9be1c-120">Messages Cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="9be1c-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="9be1c-121">Envoyer les notifications de périphérique tooa.</span><span class="sxs-lookup"><span data-stu-id="9be1c-121">Send notifications tooa device.</span></span> <span data-ttu-id="9be1c-122">Par exemple, « il est très probable toorain aujourd'hui.</span><span class="sxs-lookup"><span data-stu-id="9be1c-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="9be1c-123">N’oubliez pas toobring un parapluie. »</span><span class="sxs-lookup"><span data-stu-id="9be1c-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="9be1c-124">Requêtes de jumeaux d’appareil</span><span class="sxs-lookup"><span data-stu-id="9be1c-124">Device twin queries</span></span>        | <span data-ttu-id="9be1c-125">Requête tooretrieve de jumeaux tous les appareils dotés de conditions arbitraires, telles que l’identification des unités hello qui sont disponibles pour une utilisation.</span><span class="sxs-lookup"><span data-stu-id="9be1c-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="9be1c-126">Pour plus d’explications sur les différences de hello et des conseils sur l’utilisation de ces options, consultez [des conseils de communication de périphérique dans le cloud](iot-hub-devguide-d2c-guidance.md) et [des conseils de communication Cloud-à-appareil](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="9be1c-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9be1c-127">Les représentations d’appareil sont des documents JSON qui stockent des informations sur l’état des appareils (métadonnées, configurations et conditions).</span><span class="sxs-lookup"><span data-stu-id="9be1c-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="9be1c-128">IoT Hub conserve un double du périphérique pour chaque périphérique qui se connecte tooit.</span><span class="sxs-lookup"><span data-stu-id="9be1c-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="9be1c-129">Pour plus d’informations sur les représentations d’appareil, consultez [Prise en main des représentations d’appareils](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="9be1c-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="9be1c-130">Contenu</span><span class="sxs-lookup"><span data-stu-id="9be1c-130">What you learn</span></span>

<span data-ttu-id="9be1c-131">Vous allez apprendre à utiliser iothub-explorer avec diverses options de gestion sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="9be1c-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="9be1c-132">Procédure</span><span class="sxs-lookup"><span data-stu-id="9be1c-132">What you do</span></span>

<span data-ttu-id="9be1c-133">Exécutez iothub-diverses avec diverses options de gestion.</span><span class="sxs-lookup"><span data-stu-id="9be1c-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9be1c-134">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="9be1c-134">What you need</span></span>

- <span data-ttu-id="9be1c-135">Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="9be1c-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="9be1c-136">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="9be1c-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="9be1c-137">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9be1c-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="9be1c-138">Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="9be1c-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="9be1c-139">Assurez-vous que votre appareil est en cours d’exécution avec l’application cliente de hello au cours de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9be1c-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="9be1c-140">iothub-explorer, [Installez iothub-explorer](https://github.com/azure/iothub-explorer) sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="9be1c-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="9be1c-141">Se connecter tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="9be1c-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="9be1c-142">Se connecter tooyour IoT hub en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="9be1c-143">Utilisation d’iothub-explorer avec des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="9be1c-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="9be1c-144">Appeler hello `start` méthode hello appareil application toosend messages tooyour IoT hub en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="9be1c-145">Appeler hello `stop` méthode hello périphérique application toostop envoie des messages tooyour IoT hub en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="9be1c-146">Utiliser iothub-explorer avec les propriétés de représentation souhaitées</span><span class="sxs-lookup"><span data-stu-id="9be1c-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="9be1c-147">Définir un intervalle de la propriété désirée = 3000 en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="9be1c-148">Cette propriété peut être lue par votre appareil.</span><span class="sxs-lookup"><span data-stu-id="9be1c-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="9be1c-149">Utiliser iothub-explorer avec les propriétés signalées pour la représentation</span><span class="sxs-lookup"><span data-stu-id="9be1c-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="9be1c-150">Obtient hello signalé des propriétés du périphérique hello en exécutant hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="9be1c-151">Une des propriétés de hello est $metadata. $lastUpdated qui affiche hello dernière cet appareil envoie ou reçoit un message.</span><span class="sxs-lookup"><span data-stu-id="9be1c-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="9be1c-152">Utilisez iothub-explorer avec les balises de représentation</span><span class="sxs-lookup"><span data-stu-id="9be1c-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="9be1c-153">Afficher les étiquettes de hello et les propriétés de l’appareil de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="9be1c-154">Ajouter un rôle de champ = température et humidité appareil de toohello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="9be1c-155">Utiliser iothub-explorer avec les messages cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="9be1c-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="9be1c-156">Envoyer un périphérique toohello de message « Hello World » en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="9be1c-157">Consultez [utiliser l’Explorateur du iothub toosend et recevoir des messages entre votre appareil et un IoT Hub](iot-hub-explorer-cloud-device-messaging.md) pour un scénario réel de l’utilisation de cette commande.</span><span class="sxs-lookup"><span data-stu-id="9be1c-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="9be1c-158">Utiliser iothub-explorer avec des requêtes de représentation d’appareil</span><span class="sxs-lookup"><span data-stu-id="9be1c-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="9be1c-159">Interroger des périphériques avec une balise de rôle = « température et humidité » en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="9be1c-160">Interroger tous les périphériques à l’exception de ceux dont la balise de rôle = « température et humidité » en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9be1c-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="9be1c-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9be1c-161">Next steps</span></span>

<span data-ttu-id="9be1c-162">Vous avez appris comment toouse iothub-Explorateur avec les différentes options de gestion.</span><span class="sxs-lookup"><span data-stu-id="9be1c-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
