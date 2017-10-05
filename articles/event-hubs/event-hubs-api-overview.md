---
title: "Vue d’ensemble de l’API Azure Event Hubs | Microsoft Docs"
description: "Vue d’ensemble des API Azure Event Hubs disponibles"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 40cd76e1aacb68d6051cae4a3c90a8970f5449f0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="4a749-103">API Event Hubs disponibles</span><span class="sxs-lookup"><span data-stu-id="4a749-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="4a749-104">API de runtime</span><span class="sxs-lookup"><span data-stu-id="4a749-104">Runtime APIs</span></span>

<span data-ttu-id="4a749-105">Vous trouverez ci-dessous une description de tous les clients de runtime Azure Event Hubs actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="4a749-105">The following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="4a749-106">Bien que certaines de ces bibliothèques incluent aussi des fonctionnalités de gestion limitées, il existe [des bibliothèques](#management-apis) dédiées aux opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="4a749-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="4a749-107">Ces bibliothèques sont principalement destinées à envoyer et recevoir des messages d’un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="4a749-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="4a749-108">Consultez la section [Informations supplémentaires](#additional-information) pour plus de détails sur l’état actuel de chaque bibliothèque de runtime.</span><span class="sxs-lookup"><span data-stu-id="4a749-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="4a749-109">Langue/plateforme</span><span class="sxs-lookup"><span data-stu-id="4a749-109">Language/Platform</span></span> | <span data-ttu-id="4a749-110">Package client</span><span class="sxs-lookup"><span data-stu-id="4a749-110">Client package</span></span> | <span data-ttu-id="4a749-111">Package EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="4a749-111">EventProcessorHost package</span></span> | <span data-ttu-id="4a749-112">Référentiel</span><span class="sxs-lookup"><span data-stu-id="4a749-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4a749-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4a749-113">.NET Standard</span></span> | [<span data-ttu-id="4a749-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="4a749-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="4a749-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="4a749-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="4a749-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="4a749-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="4a749-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4a749-117">.NET Framework</span></span> | [<span data-ttu-id="4a749-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="4a749-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="4a749-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="4a749-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="4a749-120">N/A</span><span class="sxs-lookup"><span data-stu-id="4a749-120">N/A</span></span> |
| <span data-ttu-id="4a749-121">Java</span><span class="sxs-lookup"><span data-stu-id="4a749-121">Java</span></span> | [<span data-ttu-id="4a749-122">Maven</span><span class="sxs-lookup"><span data-stu-id="4a749-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="4a749-123">Maven</span><span class="sxs-lookup"><span data-stu-id="4a749-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="4a749-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="4a749-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="4a749-125">Nœud</span><span class="sxs-lookup"><span data-stu-id="4a749-125">Node</span></span> | [<span data-ttu-id="4a749-126">NPM</span><span class="sxs-lookup"><span data-stu-id="4a749-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="4a749-127">N/A</span><span class="sxs-lookup"><span data-stu-id="4a749-127">N/A</span></span> | [<span data-ttu-id="4a749-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="4a749-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="4a749-129">C</span><span class="sxs-lookup"><span data-stu-id="4a749-129">C</span></span> | <span data-ttu-id="4a749-130">N/A</span><span class="sxs-lookup"><span data-stu-id="4a749-130">N/A</span></span> | <span data-ttu-id="4a749-131">N/A</span><span class="sxs-lookup"><span data-stu-id="4a749-131">N/A</span></span> | [<span data-ttu-id="4a749-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="4a749-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="4a749-133">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4a749-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="4a749-134">.NET</span><span class="sxs-lookup"><span data-stu-id="4a749-134">.NET</span></span>
<span data-ttu-id="4a749-135">L’écosystème .NET a plusieurs runtimes, par conséquent, il existe plusieurs bibliothèques .NET pour Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4a749-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="4a749-136">La bibliothèque .NET Standard peut être exécutée à l’aide de .NET Core ou de .NET Framework, tandis que la bibliothèque .NET Framework peut uniquement être exécutée dans un environnement .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4a749-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="4a749-137">Pour plus d’informations sur .NET Framework, consultez les [versions d’infrastructure](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="4a749-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="4a749-138">Nœud</span><span class="sxs-lookup"><span data-stu-id="4a749-138">Node</span></span>

<span data-ttu-id="4a749-139">La bibliothèque Node.js est actuellement en version préliminaire et est tenue à jour en parallèle par les employés de Microsoft et des contributeurs externes.</span><span class="sxs-lookup"><span data-stu-id="4a749-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="4a749-140">Toutes les contributions, y compris le code source sont les bienvenues et seront examinées.</span><span class="sxs-lookup"><span data-stu-id="4a749-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="4a749-141">API de gestion</span><span class="sxs-lookup"><span data-stu-id="4a749-141">Management APIs</span></span>

<span data-ttu-id="4a749-142">Vous trouverez ci-dessous une liste de toutes les bibliothèques dédiées à la gestion actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="4a749-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="4a749-143">Aucune de ces bibliothèques ne contient d’opérations de runtime. Elles sont uniquement destinées à la gestion des entités Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4a749-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="4a749-144">Langue/plateforme</span><span class="sxs-lookup"><span data-stu-id="4a749-144">Language/Platform</span></span> | <span data-ttu-id="4a749-145">Gestion des packages</span><span class="sxs-lookup"><span data-stu-id="4a749-145">Management package</span></span> | <span data-ttu-id="4a749-146">Référentiel</span><span class="sxs-lookup"><span data-stu-id="4a749-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4a749-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4a749-147">.NET Standard</span></span> | [<span data-ttu-id="4a749-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="4a749-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="4a749-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="4a749-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="4a749-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4a749-150">Next steps</span></span>
<span data-ttu-id="4a749-151">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="4a749-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="4a749-152">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="4a749-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="4a749-153">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="4a749-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="4a749-154">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="4a749-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)