---
title: solutions aaaAzure pour Internet des objets (IoT Suite) | Documents Microsoft
description: "Vue d’ensemble d’un exemple d’architecture solution IoT et sa relation toodevices, hello service de Azure IoT Hub, kits de développement logiciel Azure IoT appareil, Azure IoT service SDK et autres services Azure."
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
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="c704a-103">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c704a-103">Next steps</span></span>

<span data-ttu-id="c704a-104">Azure IoT Hub est un service Azure qui autorise des communications bidirectionnelles sécurisées et fiables entre votre serveur principal de solution et des millions d’appareils.</span><span class="sxs-lookup"><span data-stu-id="c704a-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="c704a-105">Il permet de hello solution back-end à :</span><span class="sxs-lookup"><span data-stu-id="c704a-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="c704a-106">Recevoir des données de télémétrie à grande échelle en provenance de vos appareils</span><span class="sxs-lookup"><span data-stu-id="c704a-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="c704a-107">Données d’itinéraire à partir de votre processeur d’événements de périphériques tooa flux.</span><span class="sxs-lookup"><span data-stu-id="c704a-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="c704a-108">Recevoir des fichiers chargés par les appareils</span><span class="sxs-lookup"><span data-stu-id="c704a-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="c704a-109">Envoyer des messages cloud-à-appareil toospecific périphériques.</span><span class="sxs-lookup"><span data-stu-id="c704a-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="c704a-110">Vous pouvez utiliser tooimplement IoT Hub dans votre propre solution de fin.</span><span class="sxs-lookup"><span data-stu-id="c704a-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="c704a-111">En outre, IoT Hub inclut une identité Registre tooprovision des appareils, leurs informations d’identification de sécurité et leur IoT hub de droits tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="c704a-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="c704a-112">toolearn en savoir plus sur IoT Hub, consultez [Nouveautés IoT Hub ?] [lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="c704a-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="c704a-113">toolearn Azure IoT Hub permet la gestion de périphérique basé sur des normes pour vous tooremotely gérer, configurer et mettre à jour vos appareils, voir [vue d’ensemble de gestion des appareils avec IoT Hub][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="c704a-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="c704a-114">tooimplement les applications clientes sur un large éventail de plateformes d’appareils matériels et les systèmes d’exploitation, vous pouvez utiliser le dispositif de Azure IoT hello kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="c704a-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="c704a-115">Appareil de Hello SDK inclut des bibliothèques qui facilitent l’envoi télémétrie tooan IoT hub et la réception messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="c704a-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="c704a-116">Lorsque vous utilisez le périphérique hello kits de développement logiciel, vous pouvez choisir parmi plusieurs toocommunicate de protocoles de réseau avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c704a-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="c704a-117">toolearn, voir hello [plus d’informations sur les kits de développement logiciel de périphérique][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="c704a-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="c704a-118">tooget route écrire du code et en cours d’exécution des exemples, consultez hello [prise en main IoT Hub] [ lnk-getstarted] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c704a-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="c704a-119">[Azure IoT Suite][lnk-iot-suite] est un ensemble de solutions préconfigurées qui peut vous intéresser.</span><span class="sxs-lookup"><span data-stu-id="c704a-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="c704a-120">IoT Suite permet tooget démarré rapidement et l’échelle IoT projets tooaddress IoT des scénarios courants, tels que l’analyse à distance, gestion et maintenance prédictive.</span><span class="sxs-lookup"><span data-stu-id="c704a-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
