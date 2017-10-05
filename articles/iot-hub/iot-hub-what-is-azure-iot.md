---
title: "Solutions Azure pour l’Internet des objets (IoT) | Microsoft Docs"
description: "Découvrez une vue d’ensemble d’un exemple d’architecture de solution IoT et sa relation avec les appareils, le service Azure IoT Hub, les kits de développement logiciel (SDK) d’appareils Azure IoT, les kits de développement logiciel de services Azure IoT et autres services Azure."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1d54f090a0e07cd5102cb48cd70a1377845d6654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="e34b1-103">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e34b1-103">Next steps</span></span>

<span data-ttu-id="e34b1-104">Azure IoT Hub est un service Azure qui autorise des communications bidirectionnelles sécurisées et fiables entre votre serveur principal de solution et des millions d’appareils.</span><span class="sxs-lookup"><span data-stu-id="e34b1-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="e34b1-105">Grâce à ce service, le serveur de solution principal peut :</span><span class="sxs-lookup"><span data-stu-id="e34b1-105">It enables the solution back end to:</span></span>

* <span data-ttu-id="e34b1-106">Recevoir des données de télémétrie à grande échelle en provenance de vos appareils</span><span class="sxs-lookup"><span data-stu-id="e34b1-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="e34b1-107">Acheminer les données vers un processeur d’événements de flux</span><span class="sxs-lookup"><span data-stu-id="e34b1-107">Route data from your devices to a stream event processor.</span></span>
* <span data-ttu-id="e34b1-108">Recevoir des fichiers chargés par les appareils</span><span class="sxs-lookup"><span data-stu-id="e34b1-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="e34b1-109">Envoyez des messages cloud-à-appareil à des appareils spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e34b1-109">Send cloud-to-device messages to specific devices.</span></span>

<span data-ttu-id="e34b1-110">Vous pouvez utiliser IoT Hub pour implémenter votre propre serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="e34b1-110">You can use IoT Hub to implement your own solution back end.</span></span> <span data-ttu-id="e34b1-111">IoT Hub offre aussi un registre d’identités qui permet de configurer des appareils, leurs informations d’identification et leurs droits de connexion à l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e34b1-111">In addition, IoT Hub includes an identity registry used to provision devices, their security credentials, and their rights to connect to the IoT hub.</span></span> <span data-ttu-id="e34b1-112">Pour en savoir plus sur IoT Hub, consultez l’article [Qu’est-ce qu’IoT Hub ?][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="e34b1-112">To learn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="e34b1-113">Pour découvrir comment Azure IoT Hub permet une gestion des appareils basée sur des normes pour gérer, configurer et mettre à jour à distance vos appareils, consultez [Vue d’ensemble de la gestion des appareils avec IoT Hub][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="e34b1-113">To learn how Azure IoT Hub enables standards-based device management for you to remotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="e34b1-114">Pour implémenter des applications clientes sur un large éventail de plateformes matérielles et de systèmes d’exploitation d’appareils, vous pouvez utiliser les Kits de développement logiciel (SDK) d’appareils Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="e34b1-114">To implement client applications on a wide variety of device hardware platforms and operating systems, you can use the Azure IoT device SDKs.</span></span> <span data-ttu-id="e34b1-115">Le kit de développement logiciel (SDK) contient des bibliothèques qui facilitent l’envoi de télémétrie à un IoT Hub et la réception de messages cloud-vers-appareil.</span><span class="sxs-lookup"><span data-stu-id="e34b1-115">The device SDKs include libraries that facilitate sending telemetry to an IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="e34b1-116">Avec les Kits de développement logiciel (SDK) d’appareils, vous avez le choix parmi plusieurs protocoles réseau pour communiquer avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e34b1-116">When you use the device SDKs, you can choose from several network protocols to communicate with IoT Hub.</span></span> <span data-ttu-id="e34b1-117">Pour plus d’informations, consultez la rubrique [Plus d’informations sur les kits de développement logiciel (SDK) d’appareils][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="e34b1-117">To learn more, see the [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="e34b1-118">Pour commencer à écrire du code et à exécuter certains exemples, consultez le didacticiel [Prise en main d’IoT Hub][lnk-getstarted].</span><span class="sxs-lookup"><span data-stu-id="e34b1-118">To get started writing some code and running some samples, see the [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="e34b1-119">[Azure IoT Suite][lnk-iot-suite] est un ensemble de solutions préconfigurées qui peut vous intéresser.</span><span class="sxs-lookup"><span data-stu-id="e34b1-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="e34b1-120">IoT Suite vous permet de démarrer rapidement et de mettre à l’échelle des projets IoT pour résoudre des scénarios IoT courants tels que la surveillance à distance, la gestion des éléments multimédias et la maintenance prédictive.</span><span class="sxs-lookup"><span data-stu-id="e34b1-120">IoT Suite enables you to get started quickly and scale IoT projects to address common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
