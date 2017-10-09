---
title: "aaaAzure du Service d’applications et son impact sur les services Azure existants"
description: "Explique comment hello nouveau Service d’application Azure et ses fonctionnalités avoir un impact sur les services existants dans Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="67c33-103">Azure App Service et les services Azure existants</span><span class="sxs-lookup"><span data-stu-id="67c33-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="67c33-104">Cet article présente tooexisting de modifications hello services Azure dans le cadre de hello toobring de modifier simultanément plusieurs services Azure dans [Azure App Service](https://azure.microsoft.com/services/app-service/), une nouvelle offre intégrée.</span><span class="sxs-lookup"><span data-stu-id="67c33-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="67c33-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="67c33-105">Overview</span></span>
<span data-ttu-id="67c33-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) est un service de cloud de nouveaux et uniques qui permet aux développeurs toocreate applications web et mobiles pour n’importe quelle plateforme et de n’importe quel appareil.</span><span class="sxs-lookup"><span data-stu-id="67c33-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="67c33-107">Service d’applications est qu'une solution intégrée conçue de toostreamline répétée fonctions codage, intégrer à l’entreprise et les systèmes de SaaS et automatiser des processus d’entreprise tout en respectant vos besoins de sécurité, fiabilité et l’évolutivité.</span><span class="sxs-lookup"><span data-stu-id="67c33-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="67c33-108">Service d’applications réunit hello suivant Azure existants services - [sites Web](https://azure.microsoft.com/services/websites/), [Services mobiles](https://azure.microsoft.com/services/mobile-services/), et [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) en un seul combinées service, tandis que Ajout de nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="67c33-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="67c33-109">Service d’applications vous permet de hello toohost les types d’application suivants :</span><span class="sxs-lookup"><span data-stu-id="67c33-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="67c33-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="67c33-110">Web Apps</span></span>
* <span data-ttu-id="67c33-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="67c33-111">Mobile Apps</span></span>
* <span data-ttu-id="67c33-112">Applications API</span><span class="sxs-lookup"><span data-stu-id="67c33-112">API Apps</span></span>
* <span data-ttu-id="67c33-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="67c33-113">Logic Apps</span></span>

<span data-ttu-id="67c33-114">Hello tableau suivant explique comment les Azure services mappent tooApp hello application types de Service et disponibles dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="67c33-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="67c33-115">Service Azure existant</span><span class="sxs-lookup"><span data-stu-id="67c33-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="67c33-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="67c33-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="67c33-117">Ce qui a changé</span><span class="sxs-lookup"><span data-stu-id="67c33-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="67c33-118">Sites Web Azure</span><span class="sxs-lookup"><span data-stu-id="67c33-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="67c33-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="67c33-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="67c33-120">Pour les sites Web Azure, du Service d’applications est strictement limité toochanging hello nom sites Web tooWeb applications.</span><span class="sxs-lookup"><span data-stu-id="67c33-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="67c33-121">Toutes vos instances existantes de Sites Web s'appellent désormais Web Apps dans App Service.</span><span class="sxs-lookup"><span data-stu-id="67c33-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="67c33-122">Vous pouvez accéder à vos sites Web existants via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, où vous trouverez tous vos sites existants sous <em>Web Apps</em>.</span><span class="sxs-lookup"><span data-stu-id="67c33-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="67c33-123"><em>Web Plan d’hébergement</em> est désormais <em>du Plan App Service</em>.</span><span class="sxs-lookup"><span data-stu-id="67c33-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="67c33-124">Un <em>Plan App Service</em> peut héberger n’importe quel type d’application App Service (web, mobile, logique ou API).</span><span class="sxs-lookup"><span data-stu-id="67c33-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="67c33-125">Azure App Service Web Apps se trouve sous Disponibilité générale.</span><span class="sxs-lookup"><span data-stu-id="67c33-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="67c33-126"><a href="http://azure.microsoft.com/services/app-service/web/">En savoir plus sur les applications Web</a>.</span><span class="sxs-lookup"><span data-stu-id="67c33-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="67c33-127">Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="67c33-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="67c33-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="67c33-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="67c33-129">Services mobiles continuer toobe disponible en tant que service autonome et restent entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="67c33-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="67c33-130">Applications mobiles est un type d’application dans le Service d’application, qui intègre toutes les fonctionnalités de hello des Services mobiles et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="67c33-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="67c33-131">Il est facile<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrer à partir des Services mobiles tooMobile applications</a>.</span><span class="sxs-lookup"><span data-stu-id="67c33-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="67c33-132">Dans le cadre d’App Service, les applications mobiles se voient offrir de nouvelles fonctionnalités allant au-delà des services mobiles, comme l’intégration aux systèmes locaux et SaaS, les emplacements intermédiaires, WebJobs, de meilleures options de mise à l’échelle, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="67c33-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="67c33-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">En savoir plus sur les applications mobiles</a>.</span><span class="sxs-lookup"><span data-stu-id="67c33-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="67c33-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="67c33-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="67c33-135">Applications API est un nouveau type d’application dans le Service d’application qui vous permet de facilement créer et consommer des API dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="67c33-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="67c33-136"><a href="http://azure.microsoft.com/services/app-service/api/">En savoir plus sur les applications API</a>.</span><span class="sxs-lookup"><span data-stu-id="67c33-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="67c33-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="67c33-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="67c33-138">Logic Apps est un nouveau type d’application d’App Service qui permet d’automatiser les processus d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="67c33-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="67c33-139"><a href="http://azure.microsoft.com/services/app-service/logic/">En savoir plus sur les applications de la logique de</a>.</span><span class="sxs-lookup"><span data-stu-id="67c33-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="67c33-140">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="67c33-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="67c33-141">Applications API BizTalk</span><span class="sxs-lookup"><span data-stu-id="67c33-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="67c33-142">Les Services BizTalk continuer toobe disponible en tant que service autonome et restent entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="67c33-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="67c33-143">Toutes les fonctions hello des Services BizTalk sont intégrées dans du Service d’applications en tant qu’applications API permettant aux utilisateurs tooperform intégration et des scénarios d’intégration B2B avec un des types d’application hello dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="67c33-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="67c33-144">Avec les applications de la logique, vous pouvez désormais automatiser des processus d’entreprise à l’aide d’un flux de travail de conception visuelle expérience toocreate.</span><span class="sxs-lookup"><span data-stu-id="67c33-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="67c33-145">toolearn plus, visitez [documentation du Service d’application](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="67c33-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

