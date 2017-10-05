---
title: "Étapes suivantes de la création de projet Service Fabric | Microsoft Docs"
description: "Cet article contient des liens vers un ensemble de tâches de développement de base pour Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 74019850c507902d9ef7ec47a364fff234aaf32b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="62e4a-103">Votre application Service Fabric et étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62e4a-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="62e4a-104">Votre application Azure Service Fabric a été créée.</span><span class="sxs-lookup"><span data-stu-id="62e4a-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="62e4a-105">Cet article décrit la constitution de votre projet et certaines étapes futures potentielles.</span><span class="sxs-lookup"><span data-stu-id="62e4a-105">This article describes the makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="62e4a-106">Votre application.</span><span class="sxs-lookup"><span data-stu-id="62e4a-106">Your application</span></span>
<span data-ttu-id="62e4a-107">Chaque nouvelle application inclut un projet d'application.</span><span class="sxs-lookup"><span data-stu-id="62e4a-107">Every new application includes an application project.</span></span> <span data-ttu-id="62e4a-108">Il peut y avoir un ou deux projets supplémentaires en fonction du type de service choisi.</span><span class="sxs-lookup"><span data-stu-id="62e4a-108">There may be one or two additional projects, depending on the type of service chosen.</span></span>

### <a name="the-application-project"></a><span data-ttu-id="62e4a-109">Le projet d'application</span><span class="sxs-lookup"><span data-stu-id="62e4a-109">The application project</span></span>
<span data-ttu-id="62e4a-110">Le projet d'application se compose des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="62e4a-110">The application project consists of:</span></span>

* <span data-ttu-id="62e4a-111">Un ensemble de références aux services qui composent votre application.</span><span class="sxs-lookup"><span data-stu-id="62e4a-111">A set of references to the services that make up your application.</span></span>
* <span data-ttu-id="62e4a-112">Trois profils de publication (local à 1 nœud, local à 5 nœuds et cloud) que vous pouvez utiliser pour préserver les préférences d’utilisation d’environnements différents, comme les préférences liées à un point de terminaison de cluster et si vous souhaitez exécuter les déploiements de mise à niveau par défaut.</span><span class="sxs-lookup"><span data-stu-id="62e4a-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span></span>
* <span data-ttu-id="62e4a-113">Trois fichiers de paramètres d’application (du même type que ci-dessus) que vous pouvez utiliser pour gérer les configurations d’application spécifiques à l’environnement, comme le nombre de partitions à créer pour un service.</span><span class="sxs-lookup"><span data-stu-id="62e4a-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span></span>
* <span data-ttu-id="62e4a-114">Un script de déploiement que vous pouvez utiliser pour déployer votre application à partir de la ligne de commande ou dans le cadre d’un pipeline de déploiement et d’intégration continue automatisée.</span><span class="sxs-lookup"><span data-stu-id="62e4a-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="62e4a-115">Le manifeste d'application qui décrit l'application.</span><span class="sxs-lookup"><span data-stu-id="62e4a-115">The application manifest, which describes the application.</span></span> <span data-ttu-id="62e4a-116">Le manifeste se trouve dans le dossier ApplicationPackageRoot.</span><span class="sxs-lookup"><span data-stu-id="62e4a-116">You can find the manifest under the ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="62e4a-117">Service sans état</span><span class="sxs-lookup"><span data-stu-id="62e4a-117">Stateless service</span></span>
<span data-ttu-id="62e4a-118">Quand vous ajoutez un nouveau service sans état, Visual Studio ajoute un projet de service à votre solution qui inclut un type hérité de `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="62e4a-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="62e4a-119">Le service incrémente une variable locale dans un compteur.</span><span class="sxs-lookup"><span data-stu-id="62e4a-119">The service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="62e4a-120">Service avec état</span><span class="sxs-lookup"><span data-stu-id="62e4a-120">Stateful service</span></span>
<span data-ttu-id="62e4a-121">Quand vous ajoutez un nouveau service avec état, Visual Studio ajoute un projet de service à votre solution qui inclut un type hérité de `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="62e4a-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="62e4a-122">Le service incrémente un compteur dans sa méthode `RunAsync` et stocke le résultat dans un `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="62e4a-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="62e4a-123">Service d’acteur</span><span class="sxs-lookup"><span data-stu-id="62e4a-123">Actor service</span></span>
<span data-ttu-id="62e4a-124">Quand vous ajoutez un nouvel acteur fiable (Reliable Actor), Visual Studio ajoute deux projets à votre solution : un projet d’acteur et un projet d’interface.</span><span class="sxs-lookup"><span data-stu-id="62e4a-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span></span>

<span data-ttu-id="62e4a-125">Le projet d’acteur fournit des méthodes pour la définition et l’obtention de la valeur d’un compteur qui persiste de manière fiable au sein de l’état de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="62e4a-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span></span> <span data-ttu-id="62e4a-126">Le projet d'interface fournit une interface que les autres services peuvent utiliser pour appeler l'acteur.</span><span class="sxs-lookup"><span data-stu-id="62e4a-126">The interface project provides an interface that other services can use to invoke the actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="62e4a-127">API web sans état</span><span class="sxs-lookup"><span data-stu-id="62e4a-127">Stateless Web API</span></span>
<span data-ttu-id="62e4a-128">Le projet d’API web sans état fournit un service web de base que vous pouvez utiliser pour ouvrir votre application à des clients externes.</span><span class="sxs-lookup"><span data-stu-id="62e4a-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span></span> <span data-ttu-id="62e4a-129">Pour plus d’informations sur la structure du projet, consultez [Prise en main : services de l’API Web Service Fabric avec auto-hébergement OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="62e4a-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="62e4a-130">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="62e4a-130">ASP.NET core</span></span>
<span data-ttu-id="62e4a-131">Le Kit de développement logiciel (SDK) Service Fabric fournit le même ensemble de modèles ASP.NET Core que ceux disponibles pour les projets ASP.NET Core autonomes : vide, [Web API][aspnet-webapi] et [Application web][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="62e4a-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="62e4a-132">Exécutables invités et conteneurs d’invités</span><span class="sxs-lookup"><span data-stu-id="62e4a-132">Guest executables and guest containers</span></span>

<span data-ttu-id="62e4a-133">Un « invité » Service Fabric est un service qui n’est pas généré avec les modèles de programmation de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="62e4a-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span></span> <span data-ttu-id="62e4a-134">Vous pouvez empaqueter les fichiers binaires d’un invité [directement dans le package d’application](service-fabric-deploy-existing-app.md) ou [au moyen d’une image conteneur](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="62e4a-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="62e4a-135">Dans les deux cas, Visual Studio crée les artefacts nécessaires dans le dossier **ApplicationPackageRoot** du projet d’application.</span><span class="sxs-lookup"><span data-stu-id="62e4a-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span></span> <span data-ttu-id="62e4a-136">Visual Studio ne crée pas de projet de service, car le code existe déjà ailleurs.</span><span class="sxs-lookup"><span data-stu-id="62e4a-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span></span> <span data-ttu-id="62e4a-137">Si vous souhaitez gérer vos projets invités en même temps que le projet d’application Service Fabric, vous pouvez les ajouter à la même solution Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62e4a-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62e4a-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62e4a-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="62e4a-139">Création d’un cluster Azure</span><span class="sxs-lookup"><span data-stu-id="62e4a-139">Create an Azure cluster</span></span>
<span data-ttu-id="62e4a-140">Le SDK Service Fabric fournit un cluster local pour le développement et les tests.</span><span class="sxs-lookup"><span data-stu-id="62e4a-140">The Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="62e4a-141">Pour créer un cluster dans Azure, consultez [Configuration d’un cluster Service Fabric à partir du portail Azure][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="62e4a-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-to-azure"></a><span data-ttu-id="62e4a-142">Publication de votre application dans Azure</span><span class="sxs-lookup"><span data-stu-id="62e4a-142">Publish your application to Azure</span></span>
<span data-ttu-id="62e4a-143">Vous pouvez publier votre application directement à partir de Visual Studio vers un cluster Azure.</span><span class="sxs-lookup"><span data-stu-id="62e4a-143">You can publish your application directly from Visual Studio to an Azure cluster.</span></span> <span data-ttu-id="62e4a-144">Pour en savoir plus, consultez [Publication de votre application sur Azure][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="62e4a-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a><span data-ttu-id="62e4a-145">Visualisation de votre cluster à l'aide de l'outil Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="62e4a-145">Use Service Fabric Explorer to visualize your cluster</span></span>
<span data-ttu-id="62e4a-146">L’outil Service Fabric Explorer offre un moyen facile de visualiser votre cluster, notamment les applications déployées et la disposition physique.</span><span class="sxs-lookup"><span data-stu-id="62e4a-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="62e4a-147">Pour en savoir plus, consultez [Visualisation de votre cluster à l’aide de Service Fabric Explorer][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="62e4a-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="62e4a-148">Contrôle de la version et mise à niveau de vos services</span><span class="sxs-lookup"><span data-stu-id="62e4a-148">Version and upgrade your services</span></span>
<span data-ttu-id="62e4a-149">Service Fabric permet une gestion de version indépendante et la mise à niveau de services indépendants dans une application.</span><span class="sxs-lookup"><span data-stu-id="62e4a-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="62e4a-150">Pour en savoir plus, consultez [Gestion de version et mise à niveau de vos services][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="62e4a-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="62e4a-151">Configuration de l’intégration continue avec Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="62e4a-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="62e4a-152">Pour savoir comment configurer un processus d’intégration continue pour votre application Service Fabric, consultez [Configurer l’intégration continue avec Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="62e4a-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
