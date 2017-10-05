---
title: "Augmentation de l’accès concurrentiel d’un service web Azure Machine Learning | Microsoft Docs"
description: "Découvrez comment augmenter l’accès concurrentiel d’un service web Azure Machine Learning en ajoutant des points de terminaison."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "Azure Machine Learning, services web, opérationalisation, mise à l’échelle, point de terminaison, accès concurrentiel"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: 013354515d841003c912ac0338690dd975a79ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="e5455-104">Mise à l’échelle d’un service web Azure Machine Learning en ajoutant des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="e5455-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="e5455-105">Cette rubrique décrit les techniques applicables à un service web Machine Learning **classique**.</span><span class="sxs-lookup"><span data-stu-id="e5455-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="e5455-106">Par défaut, chaque service web publié est configuré pour prendre en charge 20 requêtes simultanées, avec un maximum de 200 requêtes.</span><span class="sxs-lookup"><span data-stu-id="e5455-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="e5455-107">Alors que le portail Azure Classic permet de définir cette valeur, Azure Machine Learning optimise automatiquement ce paramètre pour améliorer les performances de votre service web et la valeur de portail est ignorée.</span><span class="sxs-lookup"><span data-stu-id="e5455-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span></span> 

<span data-ttu-id="e5455-108">Si vous envisagez d’appeler l’API avec une charge supérieure à ce que le nombre maximal d’appels simultanés (200) prend en charge, vous devez créer plusieurs points de terminaison sur le même service web.</span><span class="sxs-lookup"><span data-stu-id="e5455-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span></span> <span data-ttu-id="e5455-109">Vous pouvez ensuite répartir la charge entre tous de façon aléatoire.</span><span class="sxs-lookup"><span data-stu-id="e5455-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="e5455-110">La mise à l’échelle d’un service web est une tâche courante.</span><span class="sxs-lookup"><span data-stu-id="e5455-110">The scaling of a Web service is a common task.</span></span> <span data-ttu-id="e5455-111">Parmi les raisons d’effectuer une mise à l’échelle figurent la nécessité de prendre en charge plus de 200 demandes simultanées, d’augmenter la disponibilité via plusieurs points de terminaison, ou de fournir des points de terminaison distincts pour le service web.</span><span class="sxs-lookup"><span data-stu-id="e5455-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span></span> <span data-ttu-id="e5455-112">Vous pouvez augmenter l’échelle en ajoutant des points de terminaison supplémentaires pour le même service web via le [portail Azure Classic](https://manage.windowsazure.com/) ou le portail du [service web Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="e5455-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="e5455-113">Pour plus d’informations sur l’ajout de points de terminaison, voir [Création de points de terminaison](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="e5455-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="e5455-114">N’oubliez pas que l’utilisation d’un nombre élevé d’accès concurrentiels peut être préjudiciable si vous n’appelez pas l’API avec un taux tout aussi élevé.</span><span class="sxs-lookup"><span data-stu-id="e5455-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span></span> <span data-ttu-id="e5455-115">Vous pouvez constater des délais d’attente et/ou des pics de latence sporadiques si vous placez une charge relativement faible sur une API configurée pour une charge élevée.</span><span class="sxs-lookup"><span data-stu-id="e5455-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="e5455-116">Les API synchrones sont généralement utilisées dans les situations où vous souhaitez une latence faible.</span><span class="sxs-lookup"><span data-stu-id="e5455-116">The synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="e5455-117">La latence implique ici le temps nécessaire à l’API pour compléter une demande et ne prend pas en compte les retards de réseau.</span><span class="sxs-lookup"><span data-stu-id="e5455-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="e5455-118">Supposons que vous avez une API avec une latence de 50 millisecondes.</span><span class="sxs-lookup"><span data-stu-id="e5455-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="e5455-119">Pour utiliser toute la capacité disponible avec le niveau de limitation élevé et le nombre maximal d’appels simultanés = 20, vous devez appeler cette API 20 * 1000 / 50 = 400 fois par seconde.</span><span class="sxs-lookup"><span data-stu-id="e5455-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="e5455-120">De même, un nombre maximum d’appels simultanés de 200 vous permet d’appeler l’API 4000 fois par seconde, en supposant une latence de 50 millisecondes.</span><span class="sxs-lookup"><span data-stu-id="e5455-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
