---
title: IoT Hub Azure - prise en main de la connexion de cloud de toohello appareils IoT | Documents Microsoft
description: "Découvrez comment tooconnect les starter kits tooAzure IoT Hub IoT cartes. Vos appareils peuvent envoyer la télémétrie tooIoT Hub IoT Hub peut surveiller et gérer vos appareils."
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
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="dbdb5-105">Tutoriels de prise en main d’Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="dbdb5-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="dbdb5-106">Vous pouvez utiliser Azure IoT Hub et les solutions de hello Azure IoT appareils kits de développement logiciel toobuild Internet of Things (IoT) :</span><span class="sxs-lookup"><span data-stu-id="dbdb5-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="dbdb5-107">IoT Hub Azure est un service entièrement géré dans le cloud hello qui se connecte en toute sécurité, surveille et gère vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="dbdb5-108">Utilisez hello kits de développement logiciel Azure IoT appareil tooimplement vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="dbdb5-109">Utilisez une passerelle IoT dans des scénarios IoT plus complexes.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="dbdb5-110">Par exemple, où vous devez tooconsider des facteurs tels que des périphériques hérités, les coûts de bande passante, les stratégies de sécurité et de confidentialité ou le traitement des données edge.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="dbdb5-111">Dans ces scénarios, vous utilisez Azure IoT bord tooimplement une passerelle qui se connecte IoT hub tooyour de périphériques.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="dbdb5-112">Éléments traitent dans les didacticiels hello</span><span class="sxs-lookup"><span data-stu-id="dbdb5-112">What hello tutorials cover</span></span>

<span data-ttu-id="dbdb5-113">Ces didacticiels présentent tooAzure IoT Hub et l’appareil hello kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="dbdb5-114">didacticiels de Hello couvrent les fonctionnalités courantes que IoT scénarios toodemonstrate hello de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="dbdb5-115">Hello didacticiels illustrent également la façon dont toocombine IoT Hub avec autres Azure services et les outils toobuild plus puissantes solutions IoT.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="dbdb5-116">Dans les didacticiels hello, vous pouvez choisir toouse des appareils IoT simulées ou réelles.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="dbdb5-117">En outre, vous pouvez apprendre comment toouse un IoT hub passerelle tooenable périphériques tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="dbdb5-118">Configurer votre appareil</span><span class="sxs-lookup"><span data-stu-id="dbdb5-118">Set up your device</span></span>

<span data-ttu-id="dbdb5-119">Connecter un tooAzure périphérique ou passerelle IoT IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dbdb5-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="dbdb5-120">Vous pouvez choisir un tooget périphérique physique ou simulé démarré :</span><span class="sxs-lookup"><span data-stu-id="dbdb5-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="dbdb5-121">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="dbdb5-121">IoT device</span></span>                       | <span data-ttu-id="dbdb5-122">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="dbdb5-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="dbdb5-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="dbdb5-123">Raspberry Pi</span></span>                     | <span data-ttu-id="dbdb5-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="dbdb5-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="dbdb5-125">IoT DevKit</span></span>                       | <span data-ttu-id="dbdb5-126">[Arduino dans VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="dbdb5-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="dbdb5-127">Intel Edison</span></span>                     | <span data-ttu-id="dbdb5-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="dbdb5-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="dbdb5-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="dbdb5-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="dbdb5-131">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="dbdb5-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="dbdb5-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="dbdb5-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="dbdb5-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="dbdb5-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="dbdb5-135">Appareil simulé sur PC</span><span class="sxs-lookup"><span data-stu-id="dbdb5-135">Simulated device on PC</span></span>           | <span data-ttu-id="dbdb5-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="dbdb5-137">Simulateur d’appareil en ligne</span><span class="sxs-lookup"><span data-stu-id="dbdb5-137">Online device simulator</span></span>         | <span data-ttu-id="dbdb5-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="dbdb5-139">En outre, vous pouvez utiliser un IoT hub IoT bord passerelle tooenable périphériques tooconnect tooyour :</span><span class="sxs-lookup"><span data-stu-id="dbdb5-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="dbdb5-140">Appareil de passerelle</span><span class="sxs-lookup"><span data-stu-id="dbdb5-140">Gateway device</span></span>               | <span data-ttu-id="dbdb5-141">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="dbdb5-141">Programming language</span></span> | <span data-ttu-id="dbdb5-142">Plateforme</span><span class="sxs-lookup"><span data-stu-id="dbdb5-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="dbdb5-143">Intel NUC (modèle DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="dbdb5-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="dbdb5-144">C</span><span class="sxs-lookup"><span data-stu-id="dbdb5-144">C</span></span>                    | <span data-ttu-id="dbdb5-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="dbdb5-146">Passerelle simulée</span><span class="sxs-lookup"><span data-stu-id="dbdb5-146">Simulated gateway</span></span>            | <span data-ttu-id="dbdb5-147">C</span><span class="sxs-lookup"><span data-stu-id="dbdb5-147">C</span></span>                    | <span data-ttu-id="dbdb5-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="dbdb5-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

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
