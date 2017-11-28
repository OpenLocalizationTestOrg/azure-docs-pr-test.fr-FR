---
title: "Présentation de l’API de concentrateurs d’événements aaaAzure | Documents Microsoft"
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
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="5fd19-103">API Event Hubs disponibles</span><span class="sxs-lookup"><span data-stu-id="5fd19-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="5fd19-104">API de runtime</span><span class="sxs-lookup"><span data-stu-id="5fd19-104">Runtime APIs</span></span>

<span data-ttu-id="5fd19-105">Hello Voici une description de tous les clients de runtime Azure Event Hubs actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="5fd19-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="5fd19-106">Alors que certaines de ces bibliothèques incluent également des fonctionnalités de gestion est limitée, il existe également [bibliothèques spécifiques](#management-apis) dédié toomanagement operations.</span><span class="sxs-lookup"><span data-stu-id="5fd19-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="5fd19-107">ACCENT Hello de ces bibliothèques est toosend et recevoir des messages à partir d’un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="5fd19-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="5fd19-108">Consultez [des informations supplémentaires](#additional-information) pour plus d’informations sur l’état actuel de hello de chaque bibliothèque runtime.</span><span class="sxs-lookup"><span data-stu-id="5fd19-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="5fd19-109">Langue/plateforme</span><span class="sxs-lookup"><span data-stu-id="5fd19-109">Language/Platform</span></span> | <span data-ttu-id="5fd19-110">Package client</span><span class="sxs-lookup"><span data-stu-id="5fd19-110">Client package</span></span> | <span data-ttu-id="5fd19-111">Package EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="5fd19-111">EventProcessorHost package</span></span> | <span data-ttu-id="5fd19-112">Référentiel</span><span class="sxs-lookup"><span data-stu-id="5fd19-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5fd19-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="5fd19-113">.NET Standard</span></span> | [<span data-ttu-id="5fd19-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="5fd19-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="5fd19-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="5fd19-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="5fd19-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="5fd19-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="5fd19-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5fd19-117">.NET Framework</span></span> | [<span data-ttu-id="5fd19-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="5fd19-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="5fd19-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="5fd19-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="5fd19-120">N/A</span><span class="sxs-lookup"><span data-stu-id="5fd19-120">N/A</span></span> |
| <span data-ttu-id="5fd19-121">Java</span><span class="sxs-lookup"><span data-stu-id="5fd19-121">Java</span></span> | [<span data-ttu-id="5fd19-122">Maven</span><span class="sxs-lookup"><span data-stu-id="5fd19-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="5fd19-123">Maven</span><span class="sxs-lookup"><span data-stu-id="5fd19-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="5fd19-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="5fd19-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="5fd19-125">Nœud</span><span class="sxs-lookup"><span data-stu-id="5fd19-125">Node</span></span> | [<span data-ttu-id="5fd19-126">NPM</span><span class="sxs-lookup"><span data-stu-id="5fd19-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="5fd19-127">N/A</span><span class="sxs-lookup"><span data-stu-id="5fd19-127">N/A</span></span> | [<span data-ttu-id="5fd19-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="5fd19-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="5fd19-129">C</span><span class="sxs-lookup"><span data-stu-id="5fd19-129">C</span></span> | <span data-ttu-id="5fd19-130">N/A</span><span class="sxs-lookup"><span data-stu-id="5fd19-130">N/A</span></span> | <span data-ttu-id="5fd19-131">N/A</span><span class="sxs-lookup"><span data-stu-id="5fd19-131">N/A</span></span> | [<span data-ttu-id="5fd19-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="5fd19-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="5fd19-133">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5fd19-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="5fd19-134">.NET</span><span class="sxs-lookup"><span data-stu-id="5fd19-134">.NET</span></span>
<span data-ttu-id="5fd19-135">écosystème de .NET Hello a plusieurs runtimes, par conséquent, il existe plusieurs bibliothèques .NET pour les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="5fd19-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="5fd19-136">bibliothèque .NET Standard de Hello peut être exécuté à l’aide de .NET Core ou hello .NET Framework, tandis que la bibliothèque du .NET Framework hello ne peut être exécuté dans un environnement .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5fd19-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="5fd19-137">Pour plus d’informations sur .NET Framework, consultez les [versions d’infrastructure](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="5fd19-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="5fd19-138">Nœud</span><span class="sxs-lookup"><span data-stu-id="5fd19-138">Node</span></span>

<span data-ttu-id="5fd19-139">bibliothèque de Node.js Hello est actuellement en version préliminaire et est conservée par les employés de Microsoft et des collaborateurs externes à un projet de côté.</span><span class="sxs-lookup"><span data-stu-id="5fd19-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="5fd19-140">Toutes les contributions, y compris le code source sont les bienvenues et seront examinées.</span><span class="sxs-lookup"><span data-stu-id="5fd19-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="5fd19-141">API de gestion</span><span class="sxs-lookup"><span data-stu-id="5fd19-141">Management APIs</span></span>

<span data-ttu-id="5fd19-142">Hello Voici la liste de toutes les bibliothèques spécifiques de gestion actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="5fd19-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="5fd19-143">Aucun de ces bibliothèques contiennent des opérations d’exécution et pour hello seul but de la gestion des entités de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="5fd19-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="5fd19-144">Langue/plateforme</span><span class="sxs-lookup"><span data-stu-id="5fd19-144">Language/Platform</span></span> | <span data-ttu-id="5fd19-145">Gestion des packages</span><span class="sxs-lookup"><span data-stu-id="5fd19-145">Management package</span></span> | <span data-ttu-id="5fd19-146">Référentiel</span><span class="sxs-lookup"><span data-stu-id="5fd19-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5fd19-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="5fd19-147">.NET Standard</span></span> | [<span data-ttu-id="5fd19-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="5fd19-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="5fd19-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="5fd19-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="5fd19-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5fd19-150">Next steps</span></span>
<span data-ttu-id="5fd19-151">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="5fd19-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="5fd19-152">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="5fd19-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="5fd19-153">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="5fd19-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="5fd19-154">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="5fd19-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)