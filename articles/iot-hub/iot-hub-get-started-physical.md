---
title: "Mise en route de la connexion des appareils physiques à Azure IoT Hub | Microsoft Docs"
description: "Découvrez comment connecter des cartes et des appareils physiques à Azure IoT Hub. Vos appareils peuvent envoyer des données de télémétrie à IoT Hub, et IoT Hub peut surveiller et gérer vos appareils."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: Tutoriel Azure IoT Hub
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: f4128b6b049aa876e170c56dcf2e40720644dc3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="64588-105">Didacticiels de prise en main pour les appareils physiques connectés à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="64588-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="64588-106">Ces tutoriels présentent Azure IoT Hub et les Kits de développement logiciel (SDK) d’appareil.</span><span class="sxs-lookup"><span data-stu-id="64588-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="64588-107">Les tutoriels abordent des scénarios IoT courants pour faire la démonstration des fonctionnalités de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="64588-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="64588-108">Ils illustrent également la manière dont IoT Hub peut être combiné avec d’autres services et outils Azure pour créer des solutions IoT plus puissantes.</span><span class="sxs-lookup"><span data-stu-id="64588-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="64588-109">Les didacticiels répertoriés dans le tableau ci-dessous vous montrent comment créer des appareils IoT physiques.</span><span class="sxs-lookup"><span data-stu-id="64588-109">The tutorials listed in the following table show you how to create physical IoT devices.</span></span>

| <span data-ttu-id="64588-110">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="64588-110">IoT device</span></span>                       | <span data-ttu-id="64588-111">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="64588-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="64588-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="64588-112">Raspberry Pi</span></span>                    | <span data-ttu-id="64588-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="64588-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="64588-114">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="64588-114">IoT DevKit</span></span>                      | <span data-ttu-id="64588-115">[Arduino dans VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="64588-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="64588-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="64588-116">Intel Edison</span></span>                    | <span data-ttu-id="64588-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="64588-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="64588-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="64588-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="64588-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="64588-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="64588-120">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="64588-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="64588-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="64588-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="64588-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="64588-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="64588-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="64588-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="64588-124">En outre, vous pouvez utiliser une passerelle IoT Edge pour permettre aux appareils de se connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="64588-124">In addition, you can use an IoT Edge gateway to enable devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="64588-125">Appareil de passerelle</span><span class="sxs-lookup"><span data-stu-id="64588-125">Gateway device</span></span>               | <span data-ttu-id="64588-126">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="64588-126">Programming language</span></span> | <span data-ttu-id="64588-127">Plateforme</span><span class="sxs-lookup"><span data-stu-id="64588-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="64588-128">Intel NUC (modèle DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="64588-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="64588-129">C</span><span class="sxs-lookup"><span data-stu-id="64588-129">C</span></span>                    | <span data-ttu-id="64588-130">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="64588-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
