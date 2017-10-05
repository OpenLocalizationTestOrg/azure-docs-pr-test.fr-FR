---
title: "Modèles et scénarios Azure Service Fabric | Microsoft Docs"
description: "Découvrez les meilleures pratiques et des modèles réutilisables et éprouvés pour concevoir, développer et exploiter vos microservices sur Service Fabric."
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
ms.openlocfilehash: fb2fa495758433e357722427b1c162420935955d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="40a08-103">Modèles et scénarios Service Fabric</span><span class="sxs-lookup"><span data-stu-id="40a08-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="40a08-104">Si vous souhaitez créer des microservices à grande échelle à l’aide d’Azure Service Fabric, découvrez les conseils des experts qui ont conçu et créé cette plateforme en tant que service (PaaS).</span><span class="sxs-lookup"><span data-stu-id="40a08-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from the experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="40a08-105">Prenez en main l’architecture appropriée, puis apprenez à optimiser les ressources de votre application.</span><span class="sxs-lookup"><span data-stu-id="40a08-105">Get started with proper architecture, and then learn how to optimize resources for your application.</span></span> <span data-ttu-id="40a08-106">Le cours [Modèles et meilleures pratiques pour Service Fabric](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) répond aux questions fréquemment posées par les clients du monde réel sur les scénarios et domaines d’application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="40a08-106">The [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers the questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="40a08-107">Découvrez comment concevoir, développer et exploiter vos microservices sur Service Fabric à l’aide de meilleures pratiques et de modèles réutilisables et éprouvés.</span><span class="sxs-lookup"><span data-stu-id="40a08-107">Find out how to design, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="40a08-108">Obtenez une vue d’ensemble de Service Fabric, puis approfondissez vos connaissances avec des rubriques qui couvrent la sécurité et l’optimisation du cluster, la migration des applications héritées, l’IoT à l’échelle, l’hébergement des moteurs de jeu et plus encore.</span><span class="sxs-lookup"><span data-stu-id="40a08-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="40a08-109">Découvrez la livraison continue pour différentes charges de travail, et obtenez même les détails sur la prise en charge de Linux et les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="40a08-109">Look at continuous delivery for various workloads, and even get the details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="40a08-110">Introduction</span><span class="sxs-lookup"><span data-stu-id="40a08-110">Introduction</span></span>
<span data-ttu-id="40a08-111">Découvrez les meilleures pratiques et plus d’informations sur le choix d’une plateforme en tant que service (PaaS) plutôt qu’une infrastructure en tant que service (IaaS).</span><span class="sxs-lookup"><span data-stu-id="40a08-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="40a08-112">Obtenez les détails des principes de conception d’application éprouvés suivants.</span><span class="sxs-lookup"><span data-stu-id="40a08-112">Get the details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="40a08-113">Vidéo</span><span class="sxs-lookup"><span data-stu-id="40a08-113">Video</span></span></th><th><span data-ttu-id="40a08-114">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40a08-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="40a08-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Présentation de Service Fabric</a></span><span class="sxs-lookup"><span data-stu-id="40a08-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction to Service Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="40a08-116">Planification et gestion des clusters</span><span class="sxs-lookup"><span data-stu-id="40a08-116">Cluster planning and management</span></span>
<span data-ttu-id="40a08-117">Découvrez-en davantage sur la planification de capacité et sur l’optimisation et la sécurité des clusters dans cette présentation d’Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="40a08-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="40a08-118">Vidéo</span><span class="sxs-lookup"><span data-stu-id="40a08-118">Video</span></span></th><th><span data-ttu-id="40a08-119">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40a08-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="40a08-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Planification et gestion des clusters</a></span><span class="sxs-lookup"><span data-stu-id="40a08-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="40a08-121">Web hyperscale</span><span class="sxs-lookup"><span data-stu-id="40a08-121">Hyper-scale web</span></span>
<span data-ttu-id="40a08-122">Passez en revue les concepts du web hyperscale, y compris la disponibilité et la fiabilité, l’hyperscale et la gestion des états.</span><span class="sxs-lookup"><span data-stu-id="40a08-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="40a08-123">Vidéo</span><span class="sxs-lookup"><span data-stu-id="40a08-123">Video</span></span></th><th><span data-ttu-id="40a08-124">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40a08-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="40a08-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Web hyperscale</a></span><span class="sxs-lookup"><span data-stu-id="40a08-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="40a08-126">IoT</span><span class="sxs-lookup"><span data-stu-id="40a08-126">IoT</span></span>
<span data-ttu-id="40a08-127">Explorez l’Internet des objets (IoT) dans le contexte d’Azure Service Fabric, y compris le pipeline Azure IoT, l’architecture mutualisée et l’IoT l’échelle.</span><span class="sxs-lookup"><span data-stu-id="40a08-127">Explore the Internet of Things (IoT) in the context of Azure Service Fabric, including the Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="40a08-128">Vidéo</span><span class="sxs-lookup"><span data-stu-id="40a08-128">Video</span></span></th><th><span data-ttu-id="40a08-129">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40a08-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="40a08-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="40a08-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="40a08-131">Jeux</span><span class="sxs-lookup"><span data-stu-id="40a08-131">Gaming</span></span>
<span data-ttu-id="40a08-132">Découvrez des jeux au tour par tour, des jeux interactifs et l’hébergement de moteurs de jeu existants.</span><span class="sxs-lookup"><span data-stu-id="40a08-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="40a08-133">Vidéo</span><span class="sxs-lookup"><span data-stu-id="40a08-133">Video</span></span></th><th><span data-ttu-id="40a08-134">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40a08-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="40a08-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span><span class="sxs-lookup"><span data-stu-id="40a08-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="40a08-136">Livraison continue</span><span class="sxs-lookup"><span data-stu-id="40a08-136">Continuous delivery</span></span>
<span data-ttu-id="40a08-137">Explorez les concepts, y compris la livraison/l’intégration continue avec Visual Studio Team Services, le flux de travail de génération/création de package/publication, la configuration multi-environnement et le partage/la création de packages de services.</span><span class="sxs-lookup"><span data-stu-id="40a08-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="40a08-138">Vidéo</span><span class="sxs-lookup"><span data-stu-id="40a08-138">Video</span></span></th><th><span data-ttu-id="40a08-139">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40a08-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="40a08-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Livraison continue</a></span><span class="sxs-lookup"><span data-stu-id="40a08-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="40a08-141">Migration</span><span class="sxs-lookup"><span data-stu-id="40a08-141">Migration</span></span>
<span data-ttu-id="40a08-142">Découvrez-en davantage sur la migration à partir d’un service cloud, en plus de la migration des applications héritées.</span><span class="sxs-lookup"><span data-stu-id="40a08-142">Learn about migrating from a cloud service, in addition to migration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="40a08-143">Vidéo</span><span class="sxs-lookup"><span data-stu-id="40a08-143">Video</span></span></th><th><span data-ttu-id="40a08-144">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40a08-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="40a08-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span><span class="sxs-lookup"><span data-stu-id="40a08-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="40a08-146">Prise en charge de Linux et conteneurs</span><span class="sxs-lookup"><span data-stu-id="40a08-146">Containers and Linux support</span></span>
<span data-ttu-id="40a08-147">Obtenez la réponse à la question « Pourquoi des conteneurs ? »</span><span class="sxs-lookup"><span data-stu-id="40a08-147">Get the answer to the question, "Why containers?"</span></span> <span data-ttu-id="40a08-148">Découvrez-en davantage sur la version préliminaire pour les conteneurs Windows, la prise en charge de Linux et l’orchestration de conteneurs Linux.</span><span class="sxs-lookup"><span data-stu-id="40a08-148">Learn about the preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="40a08-149">En outre, découvrez comment migrer des applications .NET Core vers Linux.</span><span class="sxs-lookup"><span data-stu-id="40a08-149">Plus, find out how to migrate .NET Core apps to Linux.</span></span>

<table><tr><th><span data-ttu-id="40a08-150">Vidéo</span><span class="sxs-lookup"><span data-stu-id="40a08-150">Video</span></span></th><th><span data-ttu-id="40a08-151">Présentation PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40a08-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="40a08-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Support Linux et conteneurs</a></span><span class="sxs-lookup"><span data-stu-id="40a08-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="40a08-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40a08-153">Next steps</span></span>
<span data-ttu-id="40a08-154">Maintenant que vous avez découvert les modèles et scénarios de Service Fabric, apprenez à [créer et gérer des clusters](service-fabric-deploy-anywhere.md), [migrer des applications de services cloud vers Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [configurer la livraison continue](service-fabric-set-up-continuous-integration.md) et [déployer des conteneurs](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40a08-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how to [create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
