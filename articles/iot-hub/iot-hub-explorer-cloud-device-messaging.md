---
title: Appareil de cloud Azure IoT Hub aaaManage messagerie avec iothub-explorer | Documents Microsoft
description: "Découvrez comment toouse hello messages toocloud (D2C) de l’appareil iothub-explorer CLI outil toomonitor et envoyer des messages de toodevice (C2D) de cloud dans Azure IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "l’Explorateur d’iothub, appareil de cloud de messagerie, iot hub cloud toodevice, cloud toodevice de messagerie"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="6e206-104">Utilisez l’Explorateur du iothub toosend et recevoir des messages entre votre appareil et un IoT Hub</span><span class="sxs-lookup"><span data-stu-id="6e206-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="6e206-106">[iothub-explorer](https://github.com/azure/iothub-explorer) dispose d’un certain nombre de commandes qui facilitent la gestion d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e206-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="6e206-107">Ce didacticiel se concentre sur la façon de toouse iothub-explorer toosend et recevoir des messages entre votre appareil et votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6e206-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6e206-108">Contenu</span><span class="sxs-lookup"><span data-stu-id="6e206-108">What you will learn</span></span>

<span data-ttu-id="6e206-109">Vous apprendrez comment toouse les messages appareil-à-cloud explorer d’iothub toomonitor et les messages de cloud-à-appareil toosend.</span><span class="sxs-lookup"><span data-stu-id="6e206-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="6e206-110">Messages appareil-à-cloud peut être des données de capteur que votre appareil collecte et envoie ensuite tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6e206-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="6e206-111">Messages cloud-à-appareil peut être votre hub IoT envoie tooyour périphérique tooblink une DEL qui est connecté tooyour périphérique de commandes.</span><span class="sxs-lookup"><span data-stu-id="6e206-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6e206-112">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="6e206-112">What you will do</span></span>

- <span data-ttu-id="6e206-113">Utilisez les messages appareil-à-cloud explorer d’iothub toomonitor.</span><span class="sxs-lookup"><span data-stu-id="6e206-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="6e206-114">Utiliser des messages de cloud-à-appareil toosend iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="6e206-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6e206-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="6e206-115">What you need</span></span>

- <span data-ttu-id="6e206-116">Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="6e206-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="6e206-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="6e206-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="6e206-118">Une instance Azure IoT Hub associée à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6e206-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="6e206-119">Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="6e206-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="6e206-120">iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="6e206-120">iothub-explorer.</span></span> <span data-ttu-id="6e206-121">([Installer iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="6e206-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="6e206-122">Analyse de messages appareil vers cloud</span><span class="sxs-lookup"><span data-stu-id="6e206-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="6e206-123">toomonitor les messages qui sont envoyés à partir de votre appareil tooyour IoT de supervision, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e206-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="6e206-124">Ouvrez une fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="6e206-124">Open a console window.</span></span>
1. <span data-ttu-id="6e206-125">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e206-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="6e206-126">Obtenez `<device-id>` et `<IoTHubConnectionString>` à partir de votre instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e206-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="6e206-127">Assurez-vous que vous avez terminé le didacticiel précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="6e206-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="6e206-128">Vous pouvez également essayer toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` si vous avez `HostName`, `SharedAccessKeyName` et `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="6e206-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="6e206-129">Envoi de messages cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="6e206-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="6e206-130">toosend un message à partir de votre appareil tooyour de hub IoT, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e206-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="6e206-131">Ouvrez une fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="6e206-131">Open a console window.</span></span>
1. <span data-ttu-id="6e206-132">Démarrer une session sur votre IoT hub en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e206-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="6e206-133">Envoyer un message de périphérique de tooyour en exécutant hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e206-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="6e206-134">commande Hello clignote hello DEL tooyour connecté appareil et envoie le dispositif de tooyour message hello.</span><span class="sxs-lookup"><span data-stu-id="6e206-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="6e206-135">Pas besoin de hello appareil toosend un accusé de réception distincts commande tooyour précédent IoT hub est lors de la réception du message de type hello.</span><span class="sxs-lookup"><span data-stu-id="6e206-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e206-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e206-136">Next steps</span></span>

<span data-ttu-id="6e206-137">Vous avez appris comment toomonitor appareil-à-cloud des messages et envoyer des messages cloud-à-appareil entre les appareils IoT Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e206-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
