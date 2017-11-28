---
title: "Vue d’ensemble de la suite Microsoft Azure IoT | Microsoft Docs"
description: "Présentation de la façon dont Azure IoT Suite offre des solutions préconfigurées de l’Internet des objets pour collecter, analyser et stocker des données, fournir des visualisations et s’intégrer à d’autres systèmes."
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
ms.openlocfilehash: bfa8dbbd0b1d943a9eb7a042df0bac25189d9ac9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="4e012-103">Vue d’ensemble de la suite Azure IoT</span><span class="sxs-lookup"><span data-stu-id="4e012-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="4e012-104">Les services Azure IoT (Internet des objets) offrent un large éventail de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="4e012-104">The Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="4e012-105">Ces services de niveau professionnel vous permettent d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4e012-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="4e012-106">Collecter des données à partir des appareils</span><span class="sxs-lookup"><span data-stu-id="4e012-106">Collect data from devices</span></span>
* <span data-ttu-id="4e012-107">Analyser les flux de données en mouvement</span><span class="sxs-lookup"><span data-stu-id="4e012-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="4e012-108">Stocker et interroger des jeux de données volumineux</span><span class="sxs-lookup"><span data-stu-id="4e012-108">Store and query large data sets</span></span>
* <span data-ttu-id="4e012-109">Visualiser les données historiques et en temps réel</span><span class="sxs-lookup"><span data-stu-id="4e012-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="4e012-110">Intégrer des systèmes back-office</span><span class="sxs-lookup"><span data-stu-id="4e012-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="4e012-111">Gestion de vos appareils</span><span class="sxs-lookup"><span data-stu-id="4e012-111">Manage your devices</span></span>

<span data-ttu-id="4e012-112">Pour fournir ces fonctionnalités, Azure IoT Suite regroupe plusieurs services Azure avec des extensions personnalisées en tant que *solutions préconfigurées*.</span><span class="sxs-lookup"><span data-stu-id="4e012-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="4e012-113">Ces solutions préconfigurées sont des implémentations de base des modèles de solution IoT courants qui aident à réduire le temps dont vous avez besoin pour fournir vos solutions IoT.</span><span class="sxs-lookup"><span data-stu-id="4e012-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="4e012-114">Les [Kits de développement logiciel IoT][lnk-sdks] vous permettent de personnaliser et d’étendre ces solutions pour répondre à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="4e012-114">Using the [IoT software development kits][lnk-sdks], you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="4e012-115">Vous pouvez également utiliser ces solutions comme des exemples ou modèles lorsque vous développez de nouvelles solutions IoT.</span><span class="sxs-lookup"><span data-stu-id="4e012-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="4e012-116">La vidéo suivante offre une présentation d’Azure IoT Suite :</span><span class="sxs-lookup"><span data-stu-id="4e012-116">The following video provides an introduction to Azure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="4e012-117">Services Azure IoT de la suite Azure IoT</span><span class="sxs-lookup"><span data-stu-id="4e012-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="4e012-118">Les solutions préconfigurées utilisent généralement les services suivants :</span><span class="sxs-lookup"><span data-stu-id="4e012-118">The preconfigured solutions typically use the following services:</span></span>

* <span data-ttu-id="4e012-119">Azure IoT Suite se situe au cœur du service [Azure IoT Hub][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="4e012-119">Core to Azure IoT Suite is the [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="4e012-120">Ce service fournit les fonctionnalités de messagerie Appareil vers cloud et Cloud vers appareil, et agit comme la passerelle vers le cloud et les autres services clés IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="4e012-120">This service provides the device-to-cloud and cloud-to-device messaging capabilities and acts as the gateway to the cloud and the other key IoT Suite services.</span></span> <span data-ttu-id="4e012-121">Le service vous permet de recevoir à grande échelle des messages provenant de vos périphériques et d’envoyer des commandes à vos périphériques.</span><span class="sxs-lookup"><span data-stu-id="4e012-121">The service enables you to receive messages from your devices at scale, and send commands to your devices.</span></span> <span data-ttu-id="4e012-122">Le service vous permet également de [gérer vos appareils][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="4e012-122">The service also enables you to [manage your devices][lnk-device-management].</span></span> <span data-ttu-id="4e012-123">Par exemple, vous pouvez configurer, redémarrer ou effectuer une réinitialisation aux paramètres d’usine sur un ou plusieurs appareils connectés au hub.</span><span class="sxs-lookup"><span data-stu-id="4e012-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected to the hub.</span></span>
* <span data-ttu-id="4e012-124">[Azure Stream Analytics][lnk-asa] fournit l’analyse des données en mouvement.</span><span class="sxs-lookup"><span data-stu-id="4e012-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="4e012-125">IoT Suite utilise ce service pour traiter la télémétrie entrante, effectuer l’agrégation et détecter les événements.</span><span class="sxs-lookup"><span data-stu-id="4e012-125">IoT Suite uses this service to process incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="4e012-126">Les solutions préconfigurées utilisent également Stream Analytics pour traiter les messages d’information qui contiennent des données telles que les réponses de métadonnées ou de commandes provenant des appareils.</span><span class="sxs-lookup"><span data-stu-id="4e012-126">The preconfigured solutions also use stream analytics to process informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="4e012-127">Les solutions utilisent Stream Analytics pour traiter les messages provenant de vos périphériques et pour remettre ces messages à d'autres services.</span><span class="sxs-lookup"><span data-stu-id="4e012-127">The solutions use Stream Analytics to process the messages from your devices and deliver those messages to other services.</span></span>
* <span data-ttu-id="4e012-128">[Stockage Azure][lnk-azure-storage] et [Azure Cosmos DB][lnk-document-db] fournissent les capacités de stockage de données.</span><span class="sxs-lookup"><span data-stu-id="4e012-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide the data storage capabilities.</span></span> <span data-ttu-id="4e012-129">Les solutions préconfigurées utilisent Blob Storage pour stocker les données de télémétrie et les rendre disponibles pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="4e012-129">The preconfigured solutions use blob storage to store telemetry and to make it available for analysis.</span></span> <span data-ttu-id="4e012-130">Les solutions utilisent Cosmos DB pour stocker les métadonnées de l’appareil et activer les fonctionnalités de gestion des appareils des solutions.</span><span class="sxs-lookup"><span data-stu-id="4e012-130">The solutions use Cosmos DB to store device metadata and enable the device management capabilities of the solutions.</span></span>
* <span data-ttu-id="4e012-131">[Azure Web Apps][lnk-web-apps] et [Microsoft Power BI][lnk-power-bi] fournissent des fonctionnalités de visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="4e012-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide the data visualization capabilities.</span></span> <span data-ttu-id="4e012-132">La flexibilité de Power BI vous permet de créer rapidement vos propres tableaux de bord interactifs utilisant des données IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="4e012-132">The flexibility of Power BI enables you to quickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="4e012-133">Pour une vue d’ensemble de l’architecture d’une solution IoT standard, consultez [Microsoft Azure et l’Internet des objets (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="4e012-133">For an overview of the architecture of a typical IoT solution, see [Microsoft Azure and the Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="4e012-134">solutions préconfigurées</span><span class="sxs-lookup"><span data-stu-id="4e012-134">Preconfigured solutions</span></span>

<span data-ttu-id="4e012-135">IoT Suite comprend des solutions préconfigurées qui vous permettent une prise en main et une exploration rapides des scénarios IoT courants comme :</span><span class="sxs-lookup"><span data-stu-id="4e012-135">IoT Suite includes preconfigured solutions that enable you to quickly get started with and to explore the common IoT scenarios, such as:</span></span>

* <span data-ttu-id="4e012-136">Surveillance à distance</span><span class="sxs-lookup"><span data-stu-id="4e012-136">Remote monitoring</span></span>
* <span data-ttu-id="4e012-137">Maintenance prédictive</span><span class="sxs-lookup"><span data-stu-id="4e012-137">Predictive maintenance</span></span>
* <span data-ttu-id="4e012-138">Fabrique connectée</span><span class="sxs-lookup"><span data-stu-id="4e012-138">Connected factory</span></span>

<span data-ttu-id="4e012-139">Vous pouvez déployer ces solutions sur votre abonnement Azure, puis exécuter un scénario IoT complet, de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="4e012-139">You can deploy these solutions to your Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e012-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e012-140">Next steps</span></span>

<span data-ttu-id="4e012-141">À présent que vous avez découvert une vue d’ensemble des fonctionnalités et des principaux composants d’IoT Suite, vous pouvez en apprendre davantage sur les solutions préconfigurées dans IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="4e012-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about the preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="4e012-142">Pour plus d’informations, consultez [Que sont les solutions préconfigurées IoT Azure ?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="4e012-142">For more information, see [What are the Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

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
