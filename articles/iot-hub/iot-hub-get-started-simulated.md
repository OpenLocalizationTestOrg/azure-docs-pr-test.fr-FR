---
title: "Prise en main de la connexion d’appareils simulés à Azure IoT Hub | Microsoft Docs"
description: "Découvrez comment créer des appareils IoT simulés et les connecter à Azure IoT Hub. Vos appareils peuvent envoyer des données de télémétrie à IoT Hub, et IoT Hub peut surveiller et gérer vos appareils."
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
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 436b3057509a831837159e814490959a2d7455a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-get-started-with-simulated-devices-tutorials"></a><span data-ttu-id="40dcd-105">Didacticiels de prise en main d’appareils simulés avec IoT Hub Azure</span><span class="sxs-lookup"><span data-stu-id="40dcd-105">Azure IoT Hub get started with simulated devices tutorials</span></span>

<span data-ttu-id="40dcd-106">Ces tutoriels présentent Azure IoT Hub et les Kits de développement logiciel (SDK) d’appareil.</span><span class="sxs-lookup"><span data-stu-id="40dcd-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="40dcd-107">Les tutoriels abordent des scénarios IoT courants pour faire la démonstration des fonctionnalités de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="40dcd-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="40dcd-108">Ils illustrent également la manière dont IoT Hub peut être combiné avec d’autres services et outils Azure pour créer des solutions IoT plus puissantes.</span><span class="sxs-lookup"><span data-stu-id="40dcd-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="40dcd-109">Les didacticiels répertoriés dans le tableau ci-dessous montrent comment créer des appareils IoT simulés.</span><span class="sxs-lookup"><span data-stu-id="40dcd-109">The tutorials listed in the following table show you how to create simulated IoT devices.</span></span>

| <span data-ttu-id="40dcd-110">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="40dcd-110">Programming language</span></span> |
|----------------------|
| <span data-ttu-id="40dcd-111">[.NET][Sim_NET]</span><span class="sxs-lookup"><span data-stu-id="40dcd-111">[.NET][Sim_NET]</span></span>      |
| <span data-ttu-id="40dcd-112">[Java][Sim_Jav]</span><span class="sxs-lookup"><span data-stu-id="40dcd-112">[Java][Sim_Jav]</span></span>      |
| <span data-ttu-id="40dcd-113">[Node.js][Sim_Nd]</span><span class="sxs-lookup"><span data-stu-id="40dcd-113">[Node.js][Sim_Nd]</span></span>    |
| <span data-ttu-id="40dcd-114">[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="40dcd-114">[Python][Sim_Pyth]</span></span>   |

<span data-ttu-id="40dcd-115">En outre, vous pouvez utiliser une passerelle IoT Edge pour permettre aux appareils simulés de se connecter à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="40dcd-115">In addition, you can use an IoT Edge gateway to enable simulated devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="40dcd-116">Langage de programmation</span><span class="sxs-lookup"><span data-stu-id="40dcd-116">Programming language</span></span> | <span data-ttu-id="40dcd-117">Plateforme</span><span class="sxs-lookup"><span data-stu-id="40dcd-117">Platform</span></span>           |
|----------------------|------------------- |
| <span data-ttu-id="40dcd-118">C</span><span class="sxs-lookup"><span data-stu-id="40dcd-118">C</span></span>                    | <span data-ttu-id="40dcd-119">[Linux][Sim_Lnx]</span><span class="sxs-lookup"><span data-stu-id="40dcd-119">[Linux][Sim_Lnx]</span></span>   |
| <span data-ttu-id="40dcd-120">C</span><span class="sxs-lookup"><span data-stu-id="40dcd-120">C</span></span>                    | <span data-ttu-id="40dcd-121">[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="40dcd-121">[Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
