---
title: aaaAzure Service Fabric sur Linux | Documents Microsoft
description: "Clusters service Fabric prend en charge Linux et Java, ce qui signifie que vous serez en mesure de toodeploy et héberger des applications de Service Fabric écrites en Java et c# sur Linux."
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
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="3d41c-103">Service Fabric sur Linux</span><span class="sxs-lookup"><span data-stu-id="3d41c-103">Service Fabric on Linux</span></span>
<span data-ttu-id="3d41c-104">Aperçu de Hello du Service Fabric sur Linux vous permet de toobuild, déployer et gérer des applications hautement disponibles et hautement évolutives sur Linux comme vous le feriez sur Windows.</span><span class="sxs-lookup"><span data-stu-id="3d41c-104">hello preview of Service Fabric on Linux enables you toobuild, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="3d41c-105">les infrastructures de Service Fabric Hello (Services fiables et Reliable Actors) sont disponibles dans Java sur Linux en outre tooC # (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="3d41c-105">hello Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition tooC# (.NET Core).</span></span>  <span data-ttu-id="3d41c-106">Vous pouvez également créer des [services exécutables invités](service-fabric-deploy-existing-app.md) via tous les langages ou frameworks.</span><span class="sxs-lookup"><span data-stu-id="3d41c-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="3d41c-107">En outre, l’aperçu de hello prend également en charge des conteneurs Docker orchestrant ces opérations.</span><span class="sxs-lookup"><span data-stu-id="3d41c-107">In addition, hello preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="3d41c-108">Conteneurs docker peuvent exécuter des exécutables de l’invité ou les services de Service Fabric natives, qui utilisent des infrastructures de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="3d41c-108">Docker containers can run guest executables or native Service Fabric services, which use hello Service Fabric frameworks.</span></span>

<span data-ttu-id="3d41c-109">Service Fabric sur Linux est conceptuellement équivalent tooService Fabric sur Windows (à l’exception des caractéristiques du système d’exploitation et la prise en charge du langage de programmation).</span><span class="sxs-lookup"><span data-stu-id="3d41c-109">Service Fabric on Linux is conceptually equivalent tooService Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="3d41c-110">Par conséquent, la plupart de nos [documentation existante](http://aka.ms/servicefabricdocs) s’applique en vous permettant de vous familiariserez avec la technologie de hello.</span><span class="sxs-lookup"><span data-stu-id="3d41c-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with hello technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="3d41c-111">Systèmes d’exploitation et langages de programmation pris en charge</span><span class="sxs-lookup"><span data-stu-id="3d41c-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="3d41c-112">Création de hello Hello limitée version préliminaire prend en charge du développement d’une case des clusters de plus toomulti-ordinateur des clusters dans Azure Ubuntu Server 16.04 en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3d41c-112">hello limited preview supports hello creation of one-box development clusters in addition toomulti-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="3d41c-113">prend en charge de la version préliminaire Hello hello Reliable Actors et hello des infrastructures de Services sans état fiable en Java et c# dans Ajout tooguest exécutables et d’organiser des conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="3d41c-113">hello preview supports hello Reliable Actors and hello Reliable Stateless Services frameworks in Java and C# in addition tooguest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="3d41c-114">Les infrastructures Reliable Collections ne sont pas encore prises en charge dans Linux.</span><span class="sxs-lookup"><span data-stu-id="3d41c-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="3d41c-115">Les clusters seuls support ne sont pas pris en charge soit - qu’une seule zone et les clusters comportant plusieurs ordinateurs Azure Linux sont prises en charge dans l’aperçu de hello.</span><span class="sxs-lookup"><span data-stu-id="3d41c-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in hello preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="3d41c-116">Outils pris en charge</span><span class="sxs-lookup"><span data-stu-id="3d41c-116">Supported tooling</span></span>
<span data-ttu-id="3d41c-117">Aperçu de Hello prend en charge l’interaction avec le cluster hello via l’interface CLI de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="3d41c-117">hello preview supports interaction with hello cluster through Service Fabric CLI.</span></span> <span data-ttu-id="3d41c-118">Pour les développeurs Java, l’intégration avec Eclipse et Yeoman est assurée, la fonction Eclipse étant prise en charge sous Linux et OSX.</span><span class="sxs-lookup"><span data-stu-id="3d41c-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="3d41c-119">Hello intégration de OSX utilise un VM Linux dans les coulisses de hello via vagrant.</span><span class="sxs-lookup"><span data-stu-id="3d41c-119">hello OSX integration uses a Linux VM under hello hood via vagrant.</span></span> <span data-ttu-id="3d41c-120">Pour les développeurs c#, l’intégration avec Yeoman est fournie toogenerate modèles d’application.</span><span class="sxs-lookup"><span data-stu-id="3d41c-120">For C# developers, integration with Yeoman is provided toogenerate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d41c-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3d41c-121">Next steps</span></span>

* <span data-ttu-id="3d41c-122">Se familiariser avec hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) et [des Services fiables](service-fabric-reliable-services-introduction.md) infrastructures de programmation</span><span class="sxs-lookup"><span data-stu-id="3d41c-122">Get familiar with hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="3d41c-123">Préparer votre environnement de développement sur Linux</span><span class="sxs-lookup"><span data-stu-id="3d41c-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="3d41c-124">Prepare your development environment on OSX (Préparer votre environnement de développement sur OSX)</span><span class="sxs-lookup"><span data-stu-id="3d41c-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="3d41c-125">Create your first Service Fabric Java application on Linux</span><span class="sxs-lookup"><span data-stu-id="3d41c-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="3d41c-126">Configurer l’intégration et le déploiement continus de Service Fabric avec Jenkins et GitHub</span><span class="sxs-lookup"><span data-stu-id="3d41c-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="3d41c-127">Différences entre Service Fabric Windows/Linux</span><span class="sxs-lookup"><span data-stu-id="3d41c-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
