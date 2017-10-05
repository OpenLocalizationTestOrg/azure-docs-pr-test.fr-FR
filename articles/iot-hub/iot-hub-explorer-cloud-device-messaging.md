---
title: "Gérer la messagerie cloud à appareil d’Azure IoT Hub avec iothub-explorer | Microsoft Docs"
description: "Découvrez comment utiliser l’outil d’interface de ligne de commande iothub-explorer pour surveiller les messages appareil vers Cloud (D2C) et l’envoi de messages Cloud vers appareil C2D dans Azure IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iothub explorer, messagerie cloud à appareil, iot hub cloud vers appareil, messagerie cloud vers appareil"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 30151b7bdc544bc36e959cc3528d37897198fc7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-iothub-explorer-to-send-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="b9632-104">Utiliser Iothub-explorer pour envoyer et recevoir des messages entre votre appareil et IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b9632-104">Use iothub-explorer to send and receive messages between your device and IoT Hub</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="b9632-106">[iothub-explorer](https://github.com/azure/iothub-explorer) dispose d’un certain nombre de commandes qui facilitent la gestion d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b9632-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="b9632-107">Ce didacticiel se concentre sur l’utilisation d’iothub-explorer pour l’envoi et la réception de messages entre votre appareil et l’instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b9632-107">This tutorial focuses on how to use iothub-explorer to send and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b9632-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="b9632-108">What you will learn</span></span>

<span data-ttu-id="b9632-109">Vous apprenez à utiliser iothub-explorer pour surveiller les messages appareil vers cloud et envoyer des messages cloud vers appareil.</span><span class="sxs-lookup"><span data-stu-id="b9632-109">You learn how to use iothub-explorer to monitor device-to-cloud messages and to send cloud-to-device messages.</span></span> <span data-ttu-id="b9632-110">Il peut s’agir de données de capteur collectées par votre appareil, puis envoyées vers votre instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b9632-110">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span></span> <span data-ttu-id="b9632-111">Il peut s’agir de commandes envoyées par votre IoT Hub à votre appareil pour faire clignoter un voyant connecté à votre appareil.</span><span class="sxs-lookup"><span data-stu-id="b9632-111">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="b9632-112">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="b9632-112">What you will do</span></span>

- <span data-ttu-id="b9632-113">Utilisez iothub-explorer pour surveiller les messages appareil vers cloud.</span><span class="sxs-lookup"><span data-stu-id="b9632-113">Use iothub-explorer to monitor device-to-cloud messages.</span></span>
- <span data-ttu-id="b9632-114">Utilisez iothub-explorer pour envoyer des messages cloud vers appareil.</span><span class="sxs-lookup"><span data-stu-id="b9632-114">Use iothub-explorer to send cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b9632-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="b9632-115">What you need</span></span>

- <span data-ttu-id="b9632-116">Le didacticiel [Configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé, qui traite des exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="b9632-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="b9632-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="b9632-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="b9632-118">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b9632-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="b9632-119">Une application cliente qui envoie des messages à votre instance Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b9632-119">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="b9632-120">iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="b9632-120">iothub-explorer.</span></span> <span data-ttu-id="b9632-121">([Installer iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="b9632-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="b9632-122">Analyse de messages appareil vers cloud</span><span class="sxs-lookup"><span data-stu-id="b9632-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="b9632-123">Pour analyser les messages envoyés à partir de votre appareil à votre instance IoT H+ub, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b9632-123">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="b9632-124">Ouvrez une fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="b9632-124">Open a console window.</span></span>
1. <span data-ttu-id="b9632-125">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b9632-125">Run the following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="b9632-126">Obtenez `<device-id>` et `<IoTHubConnectionString>` à partir de votre instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b9632-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="b9632-127">Assurez-vous d’avoir terminé le didacticiel précédent.</span><span class="sxs-lookup"><span data-stu-id="b9632-127">Make sure you've finished the previous tutorial.</span></span> <span data-ttu-id="b9632-128">Vous pouvez aussi essayer d’utiliser `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` si vous disposez de `HostName`, `SharedAccessKeyName` et `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="b9632-128">Or you can try to use `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="b9632-129">Envoi de messages cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="b9632-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="b9632-130">Pour envoyer un message à partir de votre instance IoT Hub sur votre appareil, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b9632-130">To send a message from your IoT hub to your device, follow these steps:</span></span>

1. <span data-ttu-id="b9632-131">Ouvrez une fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="b9632-131">Open a console window.</span></span>
1. <span data-ttu-id="b9632-132">Démarrez une session sur votre instance IoT Hub en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b9632-132">Start a session on your IoT hub by running the following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="b9632-133">Envoyez un message à votre appareil en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b9632-133">Send a message to your device by running the following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="b9632-134">La commande fait clignoter le voyant connecté à votre appareil et envoie le message à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="b9632-134">The command blinks the LED that is connected to your device and sends the message to your device.</span></span>

> [!Note]
> <span data-ttu-id="b9632-135">L’appareil n’a pas besoin de renvoyer de commande acquitter (ack) à votre instance IoT Hub à la réception du message.</span><span class="sxs-lookup"><span data-stu-id="b9632-135">There is no need for the device to send a separate ack command back to your IoT hub upon receiving the message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9632-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b9632-136">Next steps</span></span>

<span data-ttu-id="b9632-137">Vous avez appris à analyser des messages appareil vers cloud et à envoyer des messages cloud vers appareil entre votre appareil IoT et l’instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b9632-137">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
