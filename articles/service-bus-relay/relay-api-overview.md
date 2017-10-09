---
title: "Présentation de l’API de relais aaaAzure | Documents Microsoft"
description: "Vue d’ensemble des API Azure Relay disponibles"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="cdf05-103">API Relay disponibles</span><span class="sxs-lookup"><span data-stu-id="cdf05-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="cdf05-104">API de runtime</span><span class="sxs-lookup"><span data-stu-id="cdf05-104">Runtime APIs</span></span>

<span data-ttu-id="cdf05-105">Hello tableau suivant répertorie tous les clients de runtime de relais actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="cdf05-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="cdf05-106">Hello [des informations supplémentaires](#additional-information) section contient plus d’informations sur l’état de hello de chaque bibliothèque runtime.</span><span class="sxs-lookup"><span data-stu-id="cdf05-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="cdf05-107">Langue/plateforme</span><span class="sxs-lookup"><span data-stu-id="cdf05-107">Language/Platform</span></span> | <span data-ttu-id="cdf05-108">Fonctionnalité disponible</span><span class="sxs-lookup"><span data-stu-id="cdf05-108">Available feature</span></span> | <span data-ttu-id="cdf05-109">Package client</span><span class="sxs-lookup"><span data-stu-id="cdf05-109">Client package</span></span> | <span data-ttu-id="cdf05-110">Référentiel</span><span class="sxs-lookup"><span data-stu-id="cdf05-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cdf05-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="cdf05-111">.NET Standard</span></span> | <span data-ttu-id="cdf05-112">les connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="cdf05-112">Hybrid Connections</span></span> | [<span data-ttu-id="cdf05-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="cdf05-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="cdf05-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="cdf05-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="cdf05-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="cdf05-115">.NET Framework</span></span> | <span data-ttu-id="cdf05-116">Relais WCF</span><span class="sxs-lookup"><span data-stu-id="cdf05-116">WCF Relay</span></span> | [<span data-ttu-id="cdf05-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="cdf05-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="cdf05-118">N/A</span><span class="sxs-lookup"><span data-stu-id="cdf05-118">N/A</span></span> |
| <span data-ttu-id="cdf05-119">Nœud</span><span class="sxs-lookup"><span data-stu-id="cdf05-119">Node</span></span> | <span data-ttu-id="cdf05-120">les connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="cdf05-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="cdf05-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="cdf05-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="cdf05-122">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cdf05-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="cdf05-123">.NET</span><span class="sxs-lookup"><span data-stu-id="cdf05-123">.NET</span></span>
<span data-ttu-id="cdf05-124">écosystème de .NET Hello a plusieurs runtimes, par conséquent, il existe plusieurs bibliothèques .NET pour les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="cdf05-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="cdf05-125">bibliothèque .NET Standard de Hello peut être exécuté à l’aide de .NET Core ou hello .NET Framework, tandis que la bibliothèque du .NET Framework hello ne peut être exécuté dans un environnement .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cdf05-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="cdf05-126">Pour plus d’informations sur .NET Framework, consultez les [versions d’infrastructure](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="cdf05-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdf05-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cdf05-127">Next steps</span></span>
<span data-ttu-id="cdf05-128">toolearn en savoir plus sur Azure relais, consultez ces liens :</span><span class="sxs-lookup"><span data-stu-id="cdf05-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="cdf05-129">Qu’est-ce qu’Azure Relay ?</span><span class="sxs-lookup"><span data-stu-id="cdf05-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="cdf05-130">FAQ Relay</span><span class="sxs-lookup"><span data-stu-id="cdf05-130">Relay FAQ</span></span>](relay-faq.md)