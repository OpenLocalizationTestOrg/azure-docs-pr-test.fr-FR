---
title: "concurrence de tooincrease aaaHow d’un service web Azure Machine Learning | Documents Microsoft"
description: "Découvrez comment concurrence tooincrease d’un apprentissage Azure web service en ajoutant des points de terminaison supplémentaires."
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
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="d7c61-104">Mise à l’échelle d’un service web Azure Machine Learning en ajoutant des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="d7c61-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="d7c61-105">Cette rubrique décrit les techniques des tooa applicable **classique** service Machine Learning Web.</span><span class="sxs-lookup"><span data-stu-id="d7c61-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="d7c61-106">Par défaut, chaque service Web publié est configuré toosupport 20 requêtes simultanées et peut être aussi élevée que 200 requêtes simultanées.</span><span class="sxs-lookup"><span data-stu-id="d7c61-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="d7c61-107">Alors que hello portail classique Azure fournit un moyen tooset cette valeur, Azure Machine Learning optimise automatiquement hello paramètre tooprovide hello des performances optimales pour votre service web et valeur de portail hello est ignorée.</span><span class="sxs-lookup"><span data-stu-id="d7c61-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="d7c61-108">Si vous envisagez d’API de hello toocall avec une charge supérieure à une valeur de nombre maximal d’appels simultanés de 200 prend en charge, vous devez créer plusieurs points de terminaison sur hello même service Web.</span><span class="sxs-lookup"><span data-stu-id="d7c61-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="d7c61-109">Vous pouvez ensuite répartir la charge entre tous de façon aléatoire.</span><span class="sxs-lookup"><span data-stu-id="d7c61-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="d7c61-110">Hello mise à l’échelle d’un service Web est une tâche courante.</span><span class="sxs-lookup"><span data-stu-id="d7c61-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="d7c61-111">Certaines des raisons tooscale sont toosupport plus de 200 demandes simultanées, accroître la disponibilité par plusieurs points de terminaison ou fournir des points de terminaison distincts pour le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="d7c61-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="d7c61-112">Vous pouvez augmenter l’échelle de hello en ajoutant des points de terminaison supplémentaires pour hello même service Web via [portail Azure classic](https://manage.windowsazure.com/) ou hello [Service Web de Azure Machine Learning](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="d7c61-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="d7c61-113">Pour plus d’informations sur l’ajout de points de terminaison, voir [Création de points de terminaison](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d7c61-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="d7c61-114">Gardez à l’esprit qui peut être négatif si vous appelez pas hello API avec un taux élevé en conséquence à l’aide d’un nombre élevé d’opérations simultanées.</span><span class="sxs-lookup"><span data-stu-id="d7c61-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="d7c61-115">Vous pouvez voir des délais d’attente sporadiques et/ou des pics de latence de hello si vous placez une charge relativement faible sur une API configurée pour une charge élevée.</span><span class="sxs-lookup"><span data-stu-id="d7c61-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="d7c61-116">Hello Qu'api synchrones est généralement utilisés dans les situations où une latence faible est souhaité.</span><span class="sxs-lookup"><span data-stu-id="d7c61-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="d7c61-117">Latence ici implique des temps de hello nécessaire pour une demande d’API de hello toocomplete et les délais de réseau prise en compte.</span><span class="sxs-lookup"><span data-stu-id="d7c61-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="d7c61-118">Supposons que vous avez une API avec une latence de 50 millisecondes.</span><span class="sxs-lookup"><span data-stu-id="d7c61-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="d7c61-119">toofully consommer la capacité disponible de hello avec le niveau de limitation de bande passante élevée et le nombre maximal d’appels simultanés = 20, vous devez toocall cette API 20 * 1 000 / 50 = 400 heures par seconde.</span><span class="sxs-lookup"><span data-stu-id="d7c61-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="d7c61-120">Étendre davantage, un nombre maximal d’appels simultanés de 200 permet de vous toocall hello API 4000 fois par seconde, en supposant une latence de 50 ms.</span><span class="sxs-lookup"><span data-stu-id="d7c61-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
