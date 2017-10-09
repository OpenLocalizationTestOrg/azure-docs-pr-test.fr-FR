---
title: "Vue d’ensemble d’App Service : Azure Stack | Microsoft Docs"
description: "Vue d’ensemble d’App Service sur Azure Stack"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: 1d763f592212b3a2dcc2f03ebe317eed84e9e2de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-overview"></a><span data-ttu-id="45424-103">Vue d’ensemble d’App Service sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="45424-103">App Service on Azure Stack overview</span></span>

<span data-ttu-id="45424-104">Service d’applications Azure sur la pile de Azure est hello Azure offre de remise tooAzure pile.</span><span class="sxs-lookup"><span data-stu-id="45424-104">Azure App Service on Azure Stack is hello Azure offering brought tooAzure Stack.</span></span> <span data-ttu-id="45424-105">Hello du Service d’applications sur le programme d’installation de la pile de Azure crée hello ensemble d’instances de rôle suivant :</span><span class="sxs-lookup"><span data-stu-id="45424-105">hello App Service on Azure Stack installer creates hello following set of role instances:</span></span>

*  <span data-ttu-id="45424-106">Controller</span><span class="sxs-lookup"><span data-stu-id="45424-106">Controller</span></span>
*  <span data-ttu-id="45424-107">Gestion (deux instances sont créées)</span><span class="sxs-lookup"><span data-stu-id="45424-107">Management (two instances are created)</span></span>
*  <span data-ttu-id="45424-108">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="45424-108">FrontEnd</span></span>
*  <span data-ttu-id="45424-109">Éditeur</span><span class="sxs-lookup"><span data-stu-id="45424-109">Publisher</span></span>
*  <span data-ttu-id="45424-110">Worker (en mode Partagé)</span><span class="sxs-lookup"><span data-stu-id="45424-110">Worker (in Shared mode)</span></span>

<span data-ttu-id="45424-111">En outre, hello du Service d’applications sur le programme d’installation de la pile de Azure crée un serveur de fichiers.</span><span class="sxs-lookup"><span data-stu-id="45424-111">In addition, hello App Service on Azure Stack installer creates a file server.</span></span>
    
## <a name="whats-new-in-hello-first-release-candidate-of-app-service-on-azure-stack"></a><span data-ttu-id="45424-112">Quelles sont les nouveautés dans hello première version finale du Service d’application sur la pile de Azure ?</span><span class="sxs-lookup"><span data-stu-id="45424-112">What's new in hello first release candidate of App Service on Azure Stack?</span></span>
![Service d’applications dans le portail d’Azure pile hello][1]

<span data-ttu-id="45424-114">Hello première version finale du Service d’application sur Azure pile s’appuie sur une version préliminaire de tiers hello et apporte des améliorations et nouvelles fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="45424-114">hello first release candidate of App Service on Azure Stack builds on top of hello third preview and brings new capabilities and improvements:</span></span>

* <span data-ttu-id="45424-115">Environnements Azure Functions dans Azure Stack basés sur AD FS</span><span class="sxs-lookup"><span data-stu-id="45424-115">Azure Functions in Azure Stack environments based on Active Directory Federation Services</span></span> 
* <span data-ttu-id="45424-116">L’authentification unique prend en charge pour le portail de fonctions hello et hello des outils de développement avancées (Kudu)</span><span class="sxs-lookup"><span data-stu-id="45424-116">Single sign-on support for hello Functions portal and hello advanced developer tools (Kudu)</span></span>
* <span data-ttu-id="45424-117">Prise en charge de Java pour les applications web, mobiles et d’API</span><span class="sxs-lookup"><span data-stu-id="45424-117">Java support for web, mobile, and API applications</span></span>
* <span data-ttu-id="45424-118">Gestion des niveaux de workers à l’échelle de machines virtuelles définit les fonctionnalités de montée en puissance parallèle tooimprove aux administrateurs de service</span><span class="sxs-lookup"><span data-stu-id="45424-118">Management of worker tiers by virtual machine scale sets tooimprove scale-out capabilities for service administrators</span></span>
* <span data-ttu-id="45424-119">Localisation de l’expérience de l’administrateur hello</span><span class="sxs-lookup"><span data-stu-id="45424-119">Localization of hello admin experience</span></span>
* <span data-ttu-id="45424-120">Stabilité accrue du service de hello</span><span class="sxs-lookup"><span data-stu-id="45424-120">Increased stability of hello service</span></span>
* <span data-ttu-id="45424-121">Mises à jour de l’expérience du portail du locataire et mises à jour du processus d’installation</span><span class="sxs-lookup"><span data-stu-id="45424-121">Tenant portal experience updates and installation process updates</span></span>

## <a name="limitations-of-hello-technical-preview"></a><span data-ttu-id="45424-122">Limitations de la version d’évaluation technique hello</span><span class="sxs-lookup"><span data-stu-id="45424-122">Limitations of hello technical preview</span></span>

<span data-ttu-id="45424-123">Il n’existe aucune prise en charge pour hello du Service d’applications sur des versions préliminaires de Azure pile, bien que nous surveillez hello Forum MSDN de pile Azure.</span><span class="sxs-lookup"><span data-stu-id="45424-123">There is no support for hello App Service on Azure Stack preview releases, although we do monitor hello Azure Stack MSDN Forum.</span></span> <span data-ttu-id="45424-124">Ne placez aucune charge de travail de production dans cette préversion.</span><span class="sxs-lookup"><span data-stu-id="45424-124">Do not put production workloads on this preview release.</span></span> <span data-ttu-id="45424-125">Il n’existe également aucune mise à niveau entre les préversions App Service sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="45424-125">There is also no upgrade between App Service on Azure Stack preview releases.</span></span> <span data-ttu-id="45424-126">Hello principal à des fins de ces versions préliminaires sont tooshow que nous fournissons et tooobtain commentaires.</span><span class="sxs-lookup"><span data-stu-id="45424-126">hello primary purposes of these preview releases are tooshow what we're providing and tooobtain feedback.</span></span> 

## <a name="what-is-an-app-service-plan"></a><span data-ttu-id="45424-127">Qu’est-ce qu’un plan App Service ?</span><span class="sxs-lookup"><span data-stu-id="45424-127">What is an App Service plan?</span></span>

<span data-ttu-id="45424-128">Hello fournisseur de ressources du Service d’applications utilise hello même code que le Service d’applications Azure utilise.</span><span class="sxs-lookup"><span data-stu-id="45424-128">hello App Service resource provider uses hello same code that Azure App Service uses.</span></span> <span data-ttu-id="45424-129">Par conséquent, il peut être utile de décrire certains concepts communs.</span><span class="sxs-lookup"><span data-stu-id="45424-129">As a result, some common concepts are worth describing.</span></span> <span data-ttu-id="45424-130">Dans le Service d’application, hello tarification conteneur pour les applications est appelée hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="45424-130">In App Service, hello pricing container for applications is called hello App Service plan.</span></span> <span data-ttu-id="45424-131">Il représente le jeu hello d’utiliser des machines virtuelles dédiées toohold vos applications.</span><span class="sxs-lookup"><span data-stu-id="45424-131">It represents hello set of dedicated virtual machines used toohold your apps.</span></span> <span data-ttu-id="45424-132">Vous pouvez avoir plusieurs plans App Service dans un abonnement donné.</span><span class="sxs-lookup"><span data-stu-id="45424-132">Within a given subscription, you can have multiple App Service plans.</span></span> 

<span data-ttu-id="45424-133">Dans Azure, il existe des Workers partagés et dédiés.</span><span class="sxs-lookup"><span data-stu-id="45424-133">In Azure, there are shared and dedicated workers.</span></span> <span data-ttu-id="45424-134">Un Worker partagé prend en charge l’hébergement d’applications mutualisées à densité élevée et il n'existe qu’un seul ensemble de Workers partagés.</span><span class="sxs-lookup"><span data-stu-id="45424-134">A shared worker supports high-density multitenant app hosting, and there is only one set of shared workers.</span></span> <span data-ttu-id="45424-135">Les serveurs dédiés sont utilisés par un seul locataire et se présentent dans trois tailles : petit, moyen et grand.</span><span class="sxs-lookup"><span data-stu-id="45424-135">Dedicated servers are used by only one tenant and come in three sizes: small, medium, and large.</span></span> <span data-ttu-id="45424-136">besoins Hello de clients de locale ne peut pas toujours être décrits à l’aide de ces termes.</span><span class="sxs-lookup"><span data-stu-id="45424-136">hello needs of on-premises customers can't always be described by using those terms.</span></span> <span data-ttu-id="45424-137">Dans le Service d’application sur la pile d’Azure, administrateurs de fournisseur de ressources peuvent définir les niveaux de workers hello qu’ils souhaitent toomake disponible.</span><span class="sxs-lookup"><span data-stu-id="45424-137">In App Service on Azure Stack, resource provider administrators can define hello worker tiers they want toomake available.</span></span> <span data-ttu-id="45424-138">Les administrateurs peuvent définir plusieurs jeux de Workers partagés ou des jeux différents de Workers dédiés selon leurs besoins d’hébergements uniques.</span><span class="sxs-lookup"><span data-stu-id="45424-138">Administrators can define multiple sets of shared workers or different sets of dedicated workers based on their unique hosting needs.</span></span> <span data-ttu-id="45424-139">À l’aide de ces définitions de niveau Worker, ils peuvent ensuite définir leurs propres références de tarification.</span><span class="sxs-lookup"><span data-stu-id="45424-139">By using those worker-tier definitions, they can then define their own pricing SKUs.</span></span>

## <a name="portal-features"></a><span data-ttu-id="45424-140">Fonctionnalités du portail</span><span class="sxs-lookup"><span data-stu-id="45424-140">Portal features</span></span>

<span data-ttu-id="45424-141">Service d’applications sur Azure pile utilise hello même interface utilisateur qui utilise Azure App Service, même avec hello back end.</span><span class="sxs-lookup"><span data-stu-id="45424-141">App Service on Azure Stack uses hello same UI that Azure App Service uses, as is true with hello back end.</span></span> <span data-ttu-id="45424-142">Certaines fonctionnalités sont désactivées et ne sont pas fonctionnelles dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="45424-142">Some features are disabled and aren't functional in Azure Stack.</span></span> <span data-ttu-id="45424-143">Hello des exigences spécifiques de Azure ou services qui requièrent de ces fonctionnalités ne sont pas encore disponibles dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="45424-143">hello Azure-specific expectations or services that those features require aren't yet available in Azure Stack.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="45424-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45424-144">Next steps</span></span>

- [<span data-ttu-id="45424-145">Avant de commencer avec App Service sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="45424-145">Before you get started with App Service on Azure Stack</span></span>](azure-stack-app-service-before-you-get-started.md)
- [<span data-ttu-id="45424-146">Installer hello fournisseur de ressources du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="45424-146">Install hello App Service resource provider</span></span>](azure-stack-app-service-deploy.md)

<span data-ttu-id="45424-147">Vous pouvez également essayer l’autre [plateforme en tant que service (PaaS) services](azure-stack-tools-paas-services.md), comme hello [fournisseur de ressources SQL Server](azure-stack-sql-resource-provider-deploy.md) et hello [fournisseur de ressources MySQL](azure-stack-mysql-resource-provider-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="45424-147">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md), like hello [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and hello [MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-overview/AppService_Portal.png
