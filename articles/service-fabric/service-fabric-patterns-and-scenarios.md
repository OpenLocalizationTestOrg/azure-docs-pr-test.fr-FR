---
title: "aaaAzure Service Fabric modèles et scénarios | Documents Microsoft"
description: "Découvrez les meilleures pratiques et éprouvée, modèles réutilisable toodesign, développer et d’utiliser votre microservices sur l’infrastructure de Service."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="8a8d4-103">Modèles et scénarios Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8a8d4-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="8a8d4-104">Si vous envisagez d’utiliser à la construction de microservices à grande échelle à l’aide d’Azure Service Fabric, découvrez des experts hello qui conçus et créés de cette plateforme en tant que service (PaaS).</span><span class="sxs-lookup"><span data-stu-id="8a8d4-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from hello experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="8a8d4-105">Prise en main architecture appropriée et puis apprendre comment toooptimize des ressources pour votre application.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-105">Get started with proper architecture, and then learn how toooptimize resources for your application.</span></span> <span data-ttu-id="8a8d4-106">Hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) cours réponses hello fréquemment posées par les clients du monde réel sur les scénarios d’infrastructure de Service et les domaines d’application.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-106">hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers hello questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="8a8d4-107">Découvrez comment toodesign, développer et utiliser votre microservices sur l’infrastructure de Service à l’aide des meilleures pratiques et les modèles ayant fait leurs preuves et réutilisables.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-107">Find out how toodesign, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="8a8d4-108">Obtenez une vue d’ensemble de Service Fabric, puis approfondissez vos connaissances avec des rubriques qui couvrent la sécurité et l’optimisation du cluster, la migration des applications héritées, l’IoT à l’échelle, l’hébergement des moteurs de jeu et plus encore.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="8a8d4-109">Examinez la livraison continue pour différentes charges de travail et même hello plus d’informations sur la prise en charge de Linux et les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-109">Look at continuous delivery for various workloads, and even get hello details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="8a8d4-110">Introduction</span><span class="sxs-lookup"><span data-stu-id="8a8d4-110">Introduction</span></span>
<span data-ttu-id="8a8d4-111">Découvrez les meilleures pratiques et plus d’informations sur le choix d’une plateforme en tant que service (PaaS) plutôt qu’une infrastructure en tant que service (IaaS).</span><span class="sxs-lookup"><span data-stu-id="8a8d4-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="8a8d4-112">Obtenir les détails de hello sur les principes de conception d’application ayant fait leurs preuves suivantes.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-112">Get hello details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="8a8d4-113">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8a8d4-113">Video</span></span></th><th><span data-ttu-id="8a8d4-114">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="8a8d4-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="8a8d4-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService l’ensemble fibre optique</a></span><span class="sxs-lookup"><span data-stu-id="8a8d4-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="8a8d4-116">Planification et gestion des clusters</span><span class="sxs-lookup"><span data-stu-id="8a8d4-116">Cluster planning and management</span></span>
<span data-ttu-id="8a8d4-117">Découvrez-en davantage sur la planification de capacité et sur l’optimisation et la sécurité des clusters dans cette présentation d’Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="8a8d4-118">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8a8d4-118">Video</span></span></th><th><span data-ttu-id="8a8d4-119">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="8a8d4-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="8a8d4-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Planification et gestion des clusters</a></span><span class="sxs-lookup"><span data-stu-id="8a8d4-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="8a8d4-121">Web hyperscale</span><span class="sxs-lookup"><span data-stu-id="8a8d4-121">Hyper-scale web</span></span>
<span data-ttu-id="8a8d4-122">Passez en revue les concepts du web hyperscale, y compris la disponibilité et la fiabilité, l’hyperscale et la gestion des états.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="8a8d4-123">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8a8d4-123">Video</span></span></th><th><span data-ttu-id="8a8d4-124">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="8a8d4-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="8a8d4-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Web hyperscale</a></span><span class="sxs-lookup"><span data-stu-id="8a8d4-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="8a8d4-126">IoT</span><span class="sxs-lookup"><span data-stu-id="8a8d4-126">IoT</span></span>
<span data-ttu-id="8a8d4-127">Explorer hello Internet of Things (IoT) dans le contexte de hello d’Azure Service Fabric, y compris hello Azure IoT pipeline, une architecture mutualisée et IoT à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-127">Explore hello Internet of Things (IoT) in hello context of Azure Service Fabric, including hello Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="8a8d4-128">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8a8d4-128">Video</span></span></th><th><span data-ttu-id="8a8d4-129">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="8a8d4-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="8a8d4-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="8a8d4-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="8a8d4-131">Jeux</span><span class="sxs-lookup"><span data-stu-id="8a8d4-131">Gaming</span></span>
<span data-ttu-id="8a8d4-132">Découvrez des jeux au tour par tour, des jeux interactifs et l’hébergement de moteurs de jeu existants.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="8a8d4-133">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8a8d4-133">Video</span></span></th><th><span data-ttu-id="8a8d4-134">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="8a8d4-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="8a8d4-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span><span class="sxs-lookup"><span data-stu-id="8a8d4-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="8a8d4-136">Livraison continue</span><span class="sxs-lookup"><span data-stu-id="8a8d4-136">Continuous delivery</span></span>
<span data-ttu-id="8a8d4-137">Explorez les concepts, y compris la livraison/l’intégration continue avec Visual Studio Team Services, le flux de travail de génération/création de package/publication, la configuration multi-environnement et le partage/la création de packages de services.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="8a8d4-138">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8a8d4-138">Video</span></span></th><th><span data-ttu-id="8a8d4-139">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="8a8d4-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="8a8d4-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Livraison continue</a></span><span class="sxs-lookup"><span data-stu-id="8a8d4-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="8a8d4-141">Migration</span><span class="sxs-lookup"><span data-stu-id="8a8d4-141">Migration</span></span>
<span data-ttu-id="8a8d4-142">En savoir plus sur la migration à partir d’un service cloud, en outre toomigration des applications héritées.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-142">Learn about migrating from a cloud service, in addition toomigration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="8a8d4-143">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8a8d4-143">Video</span></span></th><th><span data-ttu-id="8a8d4-144">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="8a8d4-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="8a8d4-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span><span class="sxs-lookup"><span data-stu-id="8a8d4-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="8a8d4-146">Prise en charge de Linux et conteneurs</span><span class="sxs-lookup"><span data-stu-id="8a8d4-146">Containers and Linux support</span></span>
<span data-ttu-id="8a8d4-147">Obtenir hello répondre toohello à la question, « pourquoi conteneurs ? »</span><span class="sxs-lookup"><span data-stu-id="8a8d4-147">Get hello answer toohello question, "Why containers?"</span></span> <span data-ttu-id="8a8d4-148">En savoir plus sur Aperçu hello pour les conteneurs Windows, Linux prend en charge et d’orchestration de conteneurs Linux.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-148">Learn about hello preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="8a8d4-149">De plus, vous allez apprendre toomigrate .NET Core applications tooLinux.</span><span class="sxs-lookup"><span data-stu-id="8a8d4-149">Plus, find out how toomigrate .NET Core apps tooLinux.</span></span>

<table><tr><th><span data-ttu-id="8a8d4-150">Vidéo</span><span class="sxs-lookup"><span data-stu-id="8a8d4-150">Video</span></span></th><th><span data-ttu-id="8a8d4-151">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="8a8d4-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="8a8d4-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Support Linux et conteneurs</a></span><span class="sxs-lookup"><span data-stu-id="8a8d4-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="8a8d4-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8a8d4-153">Next steps</span></span>
<span data-ttu-id="8a8d4-154">Maintenant que vous avez appris sur les modèles de Service Fabric et les scénarios, en savoir plus sur comment trop[créer et gérer des clusters](service-fabric-deploy-anywhere.md), [migrer des applications de Services de cloud computing tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [configurer livraison continue](service-fabric-set-up-continuous-integration.md), et [déployer des conteneurs](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a8d4-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how too[create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
