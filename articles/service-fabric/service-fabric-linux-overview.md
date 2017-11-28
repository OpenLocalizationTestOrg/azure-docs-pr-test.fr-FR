---
title: Azure Service Fabric sur Linux | Microsoft Docs
description: "Les clusters Service Fabric prenant en charge Linux et Java, vous pouvez déployer et héberger des applications Service Fabric écrites en Java et C# sur Linux."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: dddc9f698d9776999d406117b46285a0f90d9620
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="d6587-103">Service Fabric sur Linux</span><span class="sxs-lookup"><span data-stu-id="d6587-103">Service Fabric on Linux</span></span>
<span data-ttu-id="d6587-104">La version d’évaluation de Service Fabric sur Linux vous permet de créer, déployer et gérer des applications à haut niveau de disponibilité et d’extensibilité dans l’environnement Linux de la même manière que sur Windows.</span><span class="sxs-lookup"><span data-stu-id="d6587-104">The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="d6587-105">De plus, les frameworks Service Fabric (Reliable Services et Reliable Actors) sont désormais disponibles dans Java sur Linux, en plus de C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="d6587-105">The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).</span></span>  <span data-ttu-id="d6587-106">Vous pouvez également créer des [services exécutables invités](service-fabric-deploy-existing-app.md) via tous les langages ou frameworks.</span><span class="sxs-lookup"><span data-stu-id="d6587-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="d6587-107">En outre, la version préliminaire prend également en charge l’orchestration des conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="d6587-107">In addition, the preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="d6587-108">Les conteneurs Docker peuvent lancer des exécutables invités ou des services Service Fabric natifs, qui ont recours à des frameworks Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d6587-108">Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks.</span></span>

<span data-ttu-id="d6587-109">Service Fabric sur Linux est conceptuellement équivalent à Service Fabric sur Windows (à l’exception des caractéristiques du système d’exploitation et de la prise en charge du langage de programmation).</span><span class="sxs-lookup"><span data-stu-id="d6587-109">Service Fabric on Linux is conceptually equivalent to Service Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="d6587-110">Par conséquent, la plupart de notre [documentation existante](http://aka.ms/servicefabricdocs) s’applique pour vous permettre de vous familiariser avec la technologie.</span><span class="sxs-lookup"><span data-stu-id="d6587-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with the technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="d6587-111">Systèmes d’exploitation et langages de programmation pris en charge</span><span class="sxs-lookup"><span data-stu-id="d6587-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="d6587-112">La version préliminaire limitée vous permet de créer des clusters de développement à boîtier unique ainsi que des clusters de plusieurs machines Azure exécutant Ubuntu Server 16.04.</span><span class="sxs-lookup"><span data-stu-id="d6587-112">The limited preview supports the creation of one-box development clusters in addition to multi-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="d6587-113">La version préliminaire prend en charge les frameworks Reliable Actors et Reliable Stateless Services dans les langages Java et C# en plus des exécutables invités et de l’orchestration de conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="d6587-113">The preview supports the Reliable Actors and the Reliable Stateless Services frameworks in Java and C# in addition to guest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="d6587-114">Les infrastructures Reliable Collections ne sont pas encore prises en charge dans Linux.</span><span class="sxs-lookup"><span data-stu-id="d6587-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="d6587-115">Par ailleurs, les clusters autonomes ne sont pas gérés. La version préliminaire ne prend en charge que les clusters impliquant plusieurs machines Linux Azure et un boîtier.</span><span class="sxs-lookup"><span data-stu-id="d6587-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in the preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="d6587-116">Outils pris en charge</span><span class="sxs-lookup"><span data-stu-id="d6587-116">Supported tooling</span></span>
<span data-ttu-id="d6587-117">L’aperçu prend en charge l’interaction avec le cluster via l’interface CLI Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d6587-117">The preview supports interaction with the cluster through Service Fabric CLI.</span></span> <span data-ttu-id="d6587-118">Pour les développeurs Java, l’intégration avec Eclipse et Yeoman est assurée, la fonction Eclipse étant prise en charge sous Linux et OSX.</span><span class="sxs-lookup"><span data-stu-id="d6587-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="d6587-119">L’intégration d’OSX repose sur une machine virtuelle Linux, via vagrant.</span><span class="sxs-lookup"><span data-stu-id="d6587-119">The OSX integration uses a Linux VM under the hood via vagrant.</span></span> <span data-ttu-id="d6587-120">Pour les développeurs C#, l’intégration avec Yeoman est assurée pour générer des modèles d’application.</span><span class="sxs-lookup"><span data-stu-id="d6587-120">For C# developers, integration with Yeoman is provided to generate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6587-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6587-121">Next steps</span></span>

* <span data-ttu-id="d6587-122">Se familiariser avec les infrastructures de programmation [Acteurs fiables](service-fabric-reliable-actors-introduction.md) et [Services fiables](service-fabric-reliable-services-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="d6587-122">Get familiar with the [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="d6587-123">Préparer votre environnement de développement sur Linux</span><span class="sxs-lookup"><span data-stu-id="d6587-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="d6587-124">Prepare your development environment on OSX (Préparer votre environnement de développement sur OSX)</span><span class="sxs-lookup"><span data-stu-id="d6587-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="d6587-125">Create your first Service Fabric Java application on Linux</span><span class="sxs-lookup"><span data-stu-id="d6587-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="d6587-126">Configurer l’intégration et le déploiement continus de Service Fabric avec Jenkins et GitHub</span><span class="sxs-lookup"><span data-stu-id="d6587-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="d6587-127">Différences entre Service Fabric Windows/Linux</span><span class="sxs-lookup"><span data-stu-id="d6587-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
