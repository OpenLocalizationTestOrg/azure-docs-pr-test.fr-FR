---
title: "Prise en main de la connexion des périphériques physiques tooAzure IoT Hub | Documents Microsoft"
description: "Découvrez comment tooconnect physique des appareils et les tableaux tooAzure IoT Hub. Vos appareils peuvent envoyer la télémétrie tooIoT Hub IoT Hub peut surveiller et gérer vos appareils."
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
ms.openlocfilehash: 47ce289c438b2f495d499d724c38ddc4b3307425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="d55a4-105">Didacticiels de prise en main pour les appareils physiques connectés à Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d55a4-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="d55a4-106">Ces didacticiels présentent tooAzure IoT Hub et l’appareil hello kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="d55a4-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="d55a4-107">didacticiels de Hello couvrent les fonctionnalités courantes que IoT scénarios toodemonstrate hello de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d55a4-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="d55a4-108">Hello didacticiels illustrent également la façon dont toocombine IoT Hub avec autres Azure services et les outils toobuild plus puissantes solutions IoT.</span><span class="sxs-lookup"><span data-stu-id="d55a4-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="d55a4-109">Hello didacticiels répertoriés dans hello tableau montrent la suite vous comment les appareils IoT physiques toocreate.</span><span class="sxs-lookup"><span data-stu-id="d55a4-109">hello tutorials listed in hello following table show you how toocreate physical IoT devices.</span></span>

| <span data-ttu-id="d55a4-110">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="d55a4-110">IoT device</span></span>                       | <span data-ttu-id="d55a4-111">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="d55a4-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="d55a4-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="d55a4-112">Raspberry Pi</span></span>                    | <span data-ttu-id="d55a4-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="d55a4-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="d55a4-114">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="d55a4-114">IoT DevKit</span></span>                      | <span data-ttu-id="d55a4-115">[Arduino dans VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="d55a4-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="d55a4-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="d55a4-116">Intel Edison</span></span>                    | <span data-ttu-id="d55a4-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="d55a4-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="d55a4-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="d55a4-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="d55a4-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="d55a4-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="d55a4-120">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="d55a4-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="d55a4-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="d55a4-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="d55a4-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="d55a4-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="d55a4-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="d55a4-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="d55a4-124">En outre, vous pouvez utiliser un IoT hub IoT bord passerelle tooenable périphériques tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="d55a4-124">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="d55a4-125">Appareil de passerelle</span><span class="sxs-lookup"><span data-stu-id="d55a4-125">Gateway device</span></span>               | <span data-ttu-id="d55a4-126">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="d55a4-126">Programming language</span></span> | <span data-ttu-id="d55a4-127">Plateforme</span><span class="sxs-lookup"><span data-stu-id="d55a4-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="d55a4-128">Intel NUC (modèle DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="d55a4-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="d55a4-129">C</span><span class="sxs-lookup"><span data-stu-id="d55a4-129">C</span></span>                    | <span data-ttu-id="d55a4-130">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="d55a4-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
