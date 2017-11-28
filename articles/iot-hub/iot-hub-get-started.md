---
title: "Azure IoT Hub : mise en route de la connexion des appareils IoT au cloud | Microsoft Docs"
description: "Découvrez comment connecter vos starter kits et cartes IoT à Azure IoT Hub. Vos appareils peuvent envoyer des données de télémétrie à IoT Hub, et IoT Hub peut surveiller et gérer vos appareils."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: Tutoriel Azure IoT Hub
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 45016e6383761ffe78f13ccef1112ab3d9753498
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="54f6a-105">Tutoriels de prise en main d’Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="54f6a-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="54f6a-106">Vous pouvez utiliser Azure IoT Hub et les Kits de développement logiciel (SDK) Azure IoT device pour générer des solutions Internet des objets (IoT) :</span><span class="sxs-lookup"><span data-stu-id="54f6a-106">You can use Azure IoT Hub and the Azure IoT device SDKs to build Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="54f6a-107">Azure IoT Hub est un service entièrement géré dans le cloud qui connecte, surveille et gère vos appareils IoT en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="54f6a-107">Azure IoT Hub is a fully managed service in the cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="54f6a-108">Utilisez les Kits de développement (SDK) d’appareil Azure IoT pour implémenter vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="54f6a-108">Use the Azure IoT Device SDKs to implement your IoT devices.</span></span>
* <span data-ttu-id="54f6a-109">Utilisez une passerelle IoT dans des scénarios IoT plus complexes.</span><span class="sxs-lookup"><span data-stu-id="54f6a-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="54f6a-110">Par exemple, dans les cas où vous devez tenir compte de facteurs tels que des périphériques d’ancienne génération, des coûts de bande passante, des stratégies de sécurité et de confidentialité ou le traitement de données edge.</span><span class="sxs-lookup"><span data-stu-id="54f6a-110">For example, where you need to consider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="54f6a-111">Dans ces scénarios, vous utilisez Azure IoT Edge pour mettre en œuvre une passerelle qui connecte des appareils à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="54f6a-111">In these scenarios, you use Azure IoT Edge to implement a gateway that connects devices to your IoT hub.</span></span>

## <a name="what-the-tutorials-cover"></a><span data-ttu-id="54f6a-112">Ce que couvrent les tutoriels</span><span class="sxs-lookup"><span data-stu-id="54f6a-112">What the tutorials cover</span></span>

<span data-ttu-id="54f6a-113">Ces tutoriels présentent Azure IoT Hub et les Kits de développement logiciel (SDK) d’appareil.</span><span class="sxs-lookup"><span data-stu-id="54f6a-113">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="54f6a-114">Les tutoriels abordent des scénarios IoT courants pour faire la démonstration des fonctionnalités de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="54f6a-114">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="54f6a-115">Ils illustrent également la manière dont IoT Hub peut être combiné avec d’autres services et outils Azure pour créer des solutions IoT plus puissantes.</span><span class="sxs-lookup"><span data-stu-id="54f6a-115">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="54f6a-116">Dans les didacticiels, vous pouvez choisir d’utiliser des appareils IoT simulés ou réels.</span><span class="sxs-lookup"><span data-stu-id="54f6a-116">In the tutorials, you can choose to use either simulated or real IoT devices.</span></span> <span data-ttu-id="54f6a-117">En outre, vous pouvez apprendre à utiliser une passerelle pour permettre aux appareils de se connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="54f6a-117">In addition, you can learn how to use a gateway to enable devices to connect to your IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="54f6a-118">Configurer votre appareil</span><span class="sxs-lookup"><span data-stu-id="54f6a-118">Set up your device</span></span>

<span data-ttu-id="54f6a-119">Configurer un appareil ou une passerelle IoT à Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="54f6a-119">Connect an IoT device or gateway to Azure IoT Hub.</span></span> <span data-ttu-id="54f6a-120">Vous pouvez choisir un appareil physique ou simulé pour commencer :</span><span class="sxs-lookup"><span data-stu-id="54f6a-120">You can choose a physical or simulated device to get started:</span></span>

| <span data-ttu-id="54f6a-121">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="54f6a-121">IoT device</span></span>                       | <span data-ttu-id="54f6a-122">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="54f6a-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="54f6a-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="54f6a-123">Raspberry Pi</span></span>                     | <span data-ttu-id="54f6a-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="54f6a-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="54f6a-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="54f6a-125">IoT DevKit</span></span>                       | <span data-ttu-id="54f6a-126">[Arduino dans VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="54f6a-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="54f6a-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="54f6a-127">Intel Edison</span></span>                     | <span data-ttu-id="54f6a-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="54f6a-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="54f6a-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="54f6a-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="54f6a-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="54f6a-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="54f6a-131">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="54f6a-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="54f6a-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="54f6a-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="54f6a-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="54f6a-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="54f6a-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="54f6a-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="54f6a-135">Appareil simulé sur PC</span><span class="sxs-lookup"><span data-stu-id="54f6a-135">Simulated device on PC</span></span>           | <span data-ttu-id="54f6a-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="54f6a-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="54f6a-137">Simulateur d’appareil en ligne</span><span class="sxs-lookup"><span data-stu-id="54f6a-137">Online device simulator</span></span>         | <span data-ttu-id="54f6a-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="54f6a-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="54f6a-139">En outre, vous pouvez utiliser une passerelle IoT Edge pour permettre à des appareils de se connecter à votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="54f6a-139">In addition, you can use an IoT Edge gateway to enable devices to connect to your IoT hub:</span></span>

| <span data-ttu-id="54f6a-140">Appareil de passerelle</span><span class="sxs-lookup"><span data-stu-id="54f6a-140">Gateway device</span></span>               | <span data-ttu-id="54f6a-141">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="54f6a-141">Programming language</span></span> | <span data-ttu-id="54f6a-142">Plateforme</span><span class="sxs-lookup"><span data-stu-id="54f6a-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="54f6a-143">Intel NUC (modèle DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="54f6a-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="54f6a-144">C</span><span class="sxs-lookup"><span data-stu-id="54f6a-144">C</span></span>                    | <span data-ttu-id="54f6a-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="54f6a-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="54f6a-146">Passerelle simulée</span><span class="sxs-lookup"><span data-stu-id="54f6a-146">Simulated gateway</span></span>            | <span data-ttu-id="54f6a-147">C</span><span class="sxs-lookup"><span data-stu-id="54f6a-147">C</span></span>                    | <span data-ttu-id="54f6a-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="54f6a-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
