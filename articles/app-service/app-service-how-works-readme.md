---
title: "fonctionnement du Service d’applications Azure aaaHow"
description: "Découvrir le fonctionnement d’App Service"
keywords: "app service, azure app service, mise à l'échelle, évolutif, plan app service, coût d'app service"
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="855d6-104">Fonctionnement d’App Service</span><span class="sxs-lookup"><span data-stu-id="855d6-104">How App Service works</span></span>
<span data-ttu-id="855d6-105">Azure App Service est un service cloud qui est conçue toosolve hello des problèmes pratiques qui ingénieurs actuels.</span><span class="sxs-lookup"><span data-stu-id="855d6-105">Azure App Service is a cloud service that's designed toosolve hello practical problems that engineers face today.</span></span>
<span data-ttu-id="855d6-106">Vues du Service d’applications sur la fourniture de la productivité des développeurs supérieure sans transiger sur hello doivent toodeliver des applications à l’échelle du cloud.</span><span class="sxs-lookup"><span data-stu-id="855d6-106">App Service focuses on providing superior developer productivity without compromising on hello need toodeliver applications at cloud scale.</span></span> 

<span data-ttu-id="855d6-107">Service d’applications fournit également des fonctionnalités de hello et infrastructures qui sont nécessaires pour créer des applications métier d’enterprise.</span><span class="sxs-lookup"><span data-stu-id="855d6-107">App Service also provides hello features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="855d6-108">Service d’applications vous permet de développer des applications dans des langages de développement les plus populaires, y compris Java, PHP, Node.js, Python et langues de Microsoft .NET hello.</span><span class="sxs-lookup"><span data-stu-id="855d6-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and hello Microsoft .NET languages.</span></span> <span data-ttu-id="855d6-109">Avec App Service, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="855d6-109">With App Service, you can:</span></span>

* <span data-ttu-id="855d6-110">générer des applications web hautement évolutives.</span><span class="sxs-lookup"><span data-stu-id="855d6-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="855d6-111">Générer rapidement des infrastructures principales d’application mobile avec un ensemble de fonctionnalités mobiles simples d’utilisation, par exemple des infrastructures principales de données, l’authentification utilisateur et les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="855d6-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="855d6-112">Implémenter, déployer et publier des API avec API Apps.</span><span class="sxs-lookup"><span data-stu-id="855d6-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="855d6-113">lier entre elles les applications métier dans des flux de travail et transformer les données avec Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="855d6-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="855d6-114">Tous les types d’applications s’appuient sur hello évolutif et flexible des applications Web platform, qui permet de toohave aux développeurs un cycle de vie optimisé expérience de gestion des applications conception tooapp.</span><span class="sxs-lookup"><span data-stu-id="855d6-114">All app types rely on hello scalable and flexible Web Apps platform, which enables developers toohave an optimized full lifecycle experience from app design tooapp maintenance.</span></span> <span data-ttu-id="855d6-115">fonctionnalités de cycle de vie Hello activer hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="855d6-115">hello lifecycle capabilities enable hello following:</span></span>

* <span data-ttu-id="855d6-116">**Création d’application rapide**.</span><span class="sxs-lookup"><span data-stu-id="855d6-116">**Quick app creation**.</span></span> <span data-ttu-id="855d6-117">Démarrer à partir de zéro ou sélectionner un package de système de prise en charge opérationnel (systèmes d’exploitation) à partir de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="855d6-117">Start from scratch or pick an operational support system (OSS) package from hello Azure Marketplace.</span></span>
* <span data-ttu-id="855d6-118">**Déploiement continu**.</span><span class="sxs-lookup"><span data-stu-id="855d6-118">**Continuous deployment**.</span></span> <span data-ttu-id="855d6-119">Déployer automatiquement un nouveau code à partir de solutions de contrôle de code source populaires comme TFS, GitHub et BitBucket, et synchroniser le contenu des services de stockage en ligne que sont OneDrive et DropBox.</span><span class="sxs-lookup"><span data-stu-id="855d6-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="855d6-120">**Tester en production**.</span><span class="sxs-lookup"><span data-stu-id="855d6-120">**Test in production**.</span></span> <span data-ttu-id="855d6-121">Facilement créer des environnements de préproduction et gérer la quantité de hello de trafic qui est en train de toothem.</span><span class="sxs-lookup"><span data-stu-id="855d6-121">Smoothly create pre-production environments and manage hello amount of traffic that's going toothem.</span></span> <span data-ttu-id="855d6-122">Débogage dans le cloud hello lorsque nécessaire et annulée lors de problèmes sont détectés.</span><span class="sxs-lookup"><span data-stu-id="855d6-122">Debug in hello cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="855d6-123">**Exécution de traitements par lots et de tâches asynchrones**.</span><span class="sxs-lookup"><span data-stu-id="855d6-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="855d6-124">Exécuter du code dans un processus en arrière-plan ou activer votre code en fonction des événements (par exemple, arrivée des messages dans Azure Storage Queue) et des heures planifiées (CRON).</span><span class="sxs-lookup"><span data-stu-id="855d6-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="855d6-125">**Mise à l’échelle application hello**.</span><span class="sxs-lookup"><span data-stu-id="855d6-125">**Scaling hello app**.</span></span> <span data-ttu-id="855d6-126">Utilisez une des nombreuses options tooautomatically faire évoluer votre service horizontalement et verticalement en fonction de l’utilisation du trafic et de ressource.</span><span class="sxs-lookup"><span data-stu-id="855d6-126">Use one of many options tooautomatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="855d6-127">Configurer des environnements privés qui sont des applications de tooyour dédié.</span><span class="sxs-lookup"><span data-stu-id="855d6-127">Configure private environments that are dedicated tooyour apps.</span></span>   
* <span data-ttu-id="855d6-128">**Mise à jour application hello**.</span><span class="sxs-lookup"><span data-stu-id="855d6-128">**Maintaining hello app**.</span></span> <span data-ttu-id="855d6-129">Utiliser un grand nombre de débogage de hello et toostay de fonctionnalités de diagnostics anticiper les problèmes et tooefficiently résoudre en temps réel (avec des fonctionnalités telles que la réparation automatique et dynamique de débogage) ou après les faits hello en analysant les journaux et mémoire fait un dump.</span><span class="sxs-lookup"><span data-stu-id="855d6-129">Use many of hello debugging and diagnostics features toostay ahead of problems and tooefficiently resolve them either in real time (with features such as auto-healing and live debugging) or after hello fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="855d6-130">Dans son ensemble, les fonctionnalités du Service d’applications activer toofocus les développeurs dans leur code et rapidement atteint un état stable et hautement évolutive de production.</span><span class="sxs-lookup"><span data-stu-id="855d6-130">As a whole, App Service capabilities enable developers toofocus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="855d6-131">Avec hello applications API et les fonctionnalités de Logic Apps, les développeurs peuvent créer des applications d’entreprise de réels pont les barrières entre les solutions d’entreprise et l’intégration de toocloud local.</span><span class="sxs-lookup"><span data-stu-id="855d6-131">With hello API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises toocloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="855d6-132">Vidéos</span><span class="sxs-lookup"><span data-stu-id="855d6-132">Videos</span></span>
* [<span data-ttu-id="855d6-133">Architecture Azure App Service</span><span class="sxs-lookup"><span data-stu-id="855d6-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="855d6-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="855d6-134">Next steps</span></span>

<span data-ttu-id="855d6-135">En savoir plus sur le Service d’application de l’une des rubriques suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="855d6-135">Learn more about App Service in one of hello following topics:</span></span>

* [<span data-ttu-id="855d6-136">Qu'est-ce qu'Azure App Service ?</span><span class="sxs-lookup"><span data-stu-id="855d6-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="855d6-137">Application web</span><span class="sxs-lookup"><span data-stu-id="855d6-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="855d6-138">Application mobile</span><span class="sxs-lookup"><span data-stu-id="855d6-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="855d6-139">Application API</span><span class="sxs-lookup"><span data-stu-id="855d6-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="855d6-140">Architecture Azure App Service (présentation)</span><span class="sxs-lookup"><span data-stu-id="855d6-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="855d6-141">Comparaison entre Azure App Service, Azure Cloud Services et Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="855d6-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="855d6-142">Présentation des plans App Service</span><span class="sxs-lookup"><span data-stu-id="855d6-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="855d6-143">Introduction tooApp environnement de Service</span><span class="sxs-lookup"><span data-stu-id="855d6-143">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="855d6-144">Exercice : création d’un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="855d6-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="855d6-145">Prise en charge des piles de développement Azure App Service</span><span class="sxs-lookup"><span data-stu-id="855d6-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



