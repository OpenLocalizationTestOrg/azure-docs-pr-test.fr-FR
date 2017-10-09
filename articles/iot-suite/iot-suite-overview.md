---
title: "vue d’ensemble de Azure IoT Suite aaaMicrosoft | Documents Microsoft"
description: "Vue d’ensemble de la façon dont Azure IoT Suite remet internet de choses solutions préconfigurées toocollect, analyser et stocker des données, fournissent des visualisations et intégrer avec d’autres systèmes."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="25a3d-103">Vue d’ensemble de la suite Azure IoT</span><span class="sxs-lookup"><span data-stu-id="25a3d-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="25a3d-104">Hello internet Azure des services de choses (IoT) offrent un large éventail de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="25a3d-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="25a3d-105">Ces services de niveau professionnel vous permettent d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="25a3d-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="25a3d-106">Collecter des données à partir des appareils</span><span class="sxs-lookup"><span data-stu-id="25a3d-106">Collect data from devices</span></span>
* <span data-ttu-id="25a3d-107">Analyser les flux de données en mouvement</span><span class="sxs-lookup"><span data-stu-id="25a3d-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="25a3d-108">Stocker et interroger des jeux de données volumineux</span><span class="sxs-lookup"><span data-stu-id="25a3d-108">Store and query large data sets</span></span>
* <span data-ttu-id="25a3d-109">Visualiser les données historiques et en temps réel</span><span class="sxs-lookup"><span data-stu-id="25a3d-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="25a3d-110">Intégrer des systèmes back-office</span><span class="sxs-lookup"><span data-stu-id="25a3d-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="25a3d-111">Gestion de vos appareils</span><span class="sxs-lookup"><span data-stu-id="25a3d-111">Manage your devices</span></span>

<span data-ttu-id="25a3d-112">toodeliver ces fonctionnalités, Azure IoT Suite packages ensemble plusieurs services Azure avec extensions personnalisées que *préconfiguré solutions*.</span><span class="sxs-lookup"><span data-stu-id="25a3d-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="25a3d-113">Ces solutions préconfigurées sont des implémentations de base des modèles de solution IoT courants qui aident à tooreduce hello le temps vous toodeliver vos solutions IoT.</span><span class="sxs-lookup"><span data-stu-id="25a3d-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="25a3d-114">À l’aide de hello [kits de développement logiciel IoT][lnk-sdks], vous pouvez personnaliser et étendre ces toomeet solutions vos propres exigences.</span><span class="sxs-lookup"><span data-stu-id="25a3d-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="25a3d-115">Vous pouvez également utiliser ces solutions comme des exemples ou modèles lorsque vous développez de nouvelles solutions IoT.</span><span class="sxs-lookup"><span data-stu-id="25a3d-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="25a3d-116">Hello vidéo suivante fournit une introduction de tooAzure IoT Suite :</span><span class="sxs-lookup"><span data-stu-id="25a3d-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="25a3d-117">Services Azure IoT de la suite Azure IoT</span><span class="sxs-lookup"><span data-stu-id="25a3d-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="25a3d-118">les solutions de Hello préconfiguré utilisent généralement hello suivant services :</span><span class="sxs-lookup"><span data-stu-id="25a3d-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="25a3d-119">Core tooAzure IoT Suite est hello [Azure IoT Hub] [ lnk-iot-hub] service.</span><span class="sxs-lookup"><span data-stu-id="25a3d-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="25a3d-120">Ce service fournit hello appareil-à-cloud et les fonctionnalités de messagerie cloud sur l’appareil et agit comme hello toohello de passerelle de cloud computing et hello autres principaux services IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="25a3d-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="25a3d-121">service de Hello vous tooreceive des messages à partir de vos appareils à grande échelle et envoyer des commandes tooyour périphériques.</span><span class="sxs-lookup"><span data-stu-id="25a3d-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="25a3d-122">service de Hello vous permet également de trop[gérer vos appareils][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="25a3d-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="25a3d-123">Par exemple, vous pouvez configurer, redémarrer ou effectuer d’usine sur un ou plusieurs hub toohello connecté de périphériques.</span><span class="sxs-lookup"><span data-stu-id="25a3d-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="25a3d-124">[Azure Stream Analytics][lnk-asa] fournit l’analyse des données en mouvement.</span><span class="sxs-lookup"><span data-stu-id="25a3d-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="25a3d-125">IoT Suite utilise ces données de télémétrie service tooprocess entrants, effectuer l’agrégation et détecter des événements.</span><span class="sxs-lookup"><span data-stu-id="25a3d-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="25a3d-126">les solutions de Hello préconfiguré utilisent également les flux analytique tooprocess messages d’information qui contiennent des données telles que les réponses de métadonnées ou une commande à partir d’appareils.</span><span class="sxs-lookup"><span data-stu-id="25a3d-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="25a3d-127">solutions de Hello utilisent des messages de type hello tooprocess Analytique de flux de données à partir de vos appareils et fournir des services de tooother de ces messages.</span><span class="sxs-lookup"><span data-stu-id="25a3d-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="25a3d-128">[Le stockage Azure] [ lnk-azure-storage] et [base de données Azure Cosmos] [ lnk-document-db] fournir des capacités de stockage de données hello.</span><span class="sxs-lookup"><span data-stu-id="25a3d-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="25a3d-129">Hello solutions préconfigurées utilisent télémétrie toostore de stockage blob et toomake disponible pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="25a3d-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="25a3d-130">solutions de Hello utilisent les métadonnées de périphérique Cosmos DB toostore et activent les fonctionnalités de gestion des appareils hello de solutions de hello.</span><span class="sxs-lookup"><span data-stu-id="25a3d-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="25a3d-131">[Azure Web Apps] [ lnk-web-apps] et [Microsoft Power BI] [ lnk-power-bi] fournir des capacités de visualisation de données hello.</span><span class="sxs-lookup"><span data-stu-id="25a3d-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="25a3d-132">flexibilité Hello de Power BI vous permet de tooquickly générer vos propres tableaux de bord interactifs qui utilisent des données IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="25a3d-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="25a3d-133">Pour une vue d’ensemble de l’architecture de hello d’une solution IoT classique, consultez [Microsoft Azure et hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="25a3d-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="25a3d-134">solutions préconfigurées</span><span class="sxs-lookup"><span data-stu-id="25a3d-134">Preconfigured solutions</span></span>

<span data-ttu-id="25a3d-135">IoT Suite inclut des solutions préconfigurées qui activer vous tooquickly prise en main et une tooexplore hello IoT les scénarios courants, tels que :</span><span class="sxs-lookup"><span data-stu-id="25a3d-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="25a3d-136">Surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="25a3d-136">Remote monitoring</span></span>
* <span data-ttu-id="25a3d-137">Maintenance prédictive</span><span class="sxs-lookup"><span data-stu-id="25a3d-137">Predictive maintenance</span></span>
* <span data-ttu-id="25a3d-138">Fabrique connectée</span><span class="sxs-lookup"><span data-stu-id="25a3d-138">Connected factory</span></span>

<span data-ttu-id="25a3d-139">Vous pouvez déployer ces solutions de tooyour abonnement Azure, puis exécutez un scénario IoT complète, de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="25a3d-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25a3d-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="25a3d-140">Next steps</span></span>

<span data-ttu-id="25a3d-141">Maintenant que vous avez une vue d’ensemble des possibilités de IoT Suite et quelles sont ses composants principaux, vous pouvez en savoir plus sur les solutions hello préconfiguré dans IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="25a3d-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="25a3d-142">Pour plus d’informations, consultez [que hello Azure IoT préconfigurées solutions ?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="25a3d-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
