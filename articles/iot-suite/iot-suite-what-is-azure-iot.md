---
title: "Solutions Azure pour l’Internet des objets (IoT) | Microsoft Docs"
description: "Une vue d’ensemble d’IoT sur Azure, avec un exemple d’architecture de solution et sa relation avec Azure IoT Hub et les solutions préconfigurées."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 437d2655-896f-4a9e-a4a8-b864790d3ef8
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 320190488bb4c7b8192421f9dd50a5264f558584
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="azure-iot-suite"></a><span data-ttu-id="0e709-103">Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="0e709-103">Azure IoT Suite</span></span>
<span data-ttu-id="0e709-104">Microsoft Azure IoT Suite est une solution d’entreprise qui permet une prise en main rapide grâce à un ensemble de solutions préconfigurées extensibles.</span><span class="sxs-lookup"><span data-stu-id="0e709-104">The Microsoft Azure IoT Suite is an enterprise-grade solution that enables you to get started quickly through a set of extensible preconfigured solutions.</span></span> <span data-ttu-id="0e709-105">Ces solutions sont conçues pour couvrir la plupart des scénarios IoT comme la [surveillance à distance][lnk-preconfigured-solutions], la [maintenance prédictive][lnk-predictive-maintenance] et la [fabrique connectée][lnk-connected-factory].</span><span class="sxs-lookup"><span data-stu-id="0e709-105">These solutions address common IoT scenarios, such as [remote monitoring][lnk-preconfigured-solutions], [predictive maintenance][lnk-predictive-maintenance], and [connected factory][lnk-connected-factory].</span></span> <span data-ttu-id="0e709-106">Ces solutions sont des implémentations de l’architecture de solution IoT décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="0e709-106">These solutions are implementations of the IoT solution architecture outlined in this article.</span></span>

<span data-ttu-id="0e709-107">Les solutions préconfigurées sont des solutions complètes fonctionnant de bout en bout qui incluent :</span><span class="sxs-lookup"><span data-stu-id="0e709-107">The preconfigured solutions are complete, working, end-to-end solutions that include:</span></span>

- <span data-ttu-id="0e709-108">des simulations d’appareils pour faciliter la prise en main ;</span><span class="sxs-lookup"><span data-stu-id="0e709-108">Simulated devices to get you started.</span></span>
- <span data-ttu-id="0e709-109">Les services Azure préconfigurés tels que [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning] et [Stockage Azure][Azure storage].</span><span class="sxs-lookup"><span data-stu-id="0e709-109">Preconfigured Azure services such as [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning], and [Azure storage][Azure storage].</span></span>
- <span data-ttu-id="0e709-110">des consoles de gestion de solutions spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0e709-110">Solution-specific management consoles.</span></span>

<span data-ttu-id="0e709-111">Les solutions préconfigurées contiennent du code éprouvé, prêt pour la production, que vous pouvez personnaliser et étendre pour implémenter vos propres scénarios IoT spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0e709-111">The preconfigured solutions contain proven, production-ready code that you can customize and extend to implement your own specific IoT scenarios.</span></span>

<span data-ttu-id="0e709-112">Vous pouvez également être intéressé par le service [Azure IoT Hub][Azure IoT Hub], utilisé par un grand nombre de solutions préconfigurées.</span><span class="sxs-lookup"><span data-stu-id="0e709-112">You may also be interested in the [Azure IoT Hub][Azure IoT Hub] service that many of the preconfigured solutions use.</span></span> <span data-ttu-id="0e709-113">[Azure IoT Hub][Azure IoT Hub] établit une communication bidirectionnelle sécurisée et fiable entre les appareils et le cloud utilisé dans l’architecture de solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="0e709-113">[Azure IoT Hub][Azure IoT Hub] provides the secure and reliable bi-directional communications between devices and the cloud used in the preconfigured solution architecture.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e709-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e709-114">Next steps</span></span>
<span data-ttu-id="0e709-115">Explorez les ressources ci-après pour en savoir plus sur IoT Suite et sur les solutions préconfigurées :</span><span class="sxs-lookup"><span data-stu-id="0e709-115">Explore these resources to continue learning about IoT Suite and the preconfigured solutions:</span></span>

* <span data-ttu-id="0e709-116">[Qu’est-ce qu’Azure IoT Suite ?][lnk-whatissuite]</span><span class="sxs-lookup"><span data-stu-id="0e709-116">[What is Azure IoT Suite?][lnk-whatissuite]</span></span>
* <span data-ttu-id="0e709-117">[Que sont les solutions préconfigurées Azure IoT Suite ?][lnk-whatarepreconfigured]</span><span class="sxs-lookup"><span data-stu-id="0e709-117">[What are the Azure IoT Suite preconfigured solutions?][lnk-whatarepreconfigured]</span></span>

[lnk-whatissuite]: iot-suite-overview.md
[lnk-whatarepreconfigured]: iot-suite-what-are-preconfigured-solutions.md

[lnk-preconfigured-solutions]: iot-suite-getstarted-preconfigured-solutions.md
[Azure IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[Azure Event Hubs]: https://azure.microsoft.com/documentation/services/event-hubs/
[Azure Stream Analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[Azure Machine Learning]: https://azure.microsoft.com/documentation/services/machine-learning/
[Azure storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-connected-factory]: iot-suite-connected-factory-overview.md