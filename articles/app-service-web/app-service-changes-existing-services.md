---
title: "Azure App Service et son impact sur les services Azure existants"
description: "Explique l'impact d'Azure App Service et de ses fonctionnalités sur les services existants d'Azure."
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
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="dbceb-103">Azure App Service et les services Azure existants</span><span class="sxs-lookup"><span data-stu-id="dbceb-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="dbceb-104">Cet article présente les modifications apportées aux services Azure existants dans le cadre du regroupement de plusieurs services Azure au sein d’ [Azure App Service](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="dbceb-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="dbceb-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dbceb-105">Overview</span></span>
<span data-ttu-id="dbceb-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) est un nouveau service cloud qui permet aux développeurs de créer des applications web et mobiles pour toutes les plateformes et tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="dbceb-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="dbceb-107">App Service est une solution intégrée conçue pour simplifier les fonctions de codage répétées. Elle s'intègre aux systèmes entreprise et SaaS, et automatise les processus métier tout en répondant à vos besoins en matière de sécurité, de fiabilité et d'évolutivité.</span><span class="sxs-lookup"><span data-stu-id="dbceb-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="dbceb-108">App Service réunit les services Azure existants, [Sites Web](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/) et [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) en un seul et même service, tout en y ajoutant de nouvelles fonctionnalités puissantes.</span><span class="sxs-lookup"><span data-stu-id="dbceb-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="dbceb-109">App Service vous permet d'héberger les types d'applications suivants :</span><span class="sxs-lookup"><span data-stu-id="dbceb-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="dbceb-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="dbceb-110">Web Apps</span></span>
* <span data-ttu-id="dbceb-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="dbceb-111">Mobile Apps</span></span>
* <span data-ttu-id="dbceb-112">Applications API</span><span class="sxs-lookup"><span data-stu-id="dbceb-112">API Apps</span></span>
* <span data-ttu-id="dbceb-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="dbceb-113">Logic Apps</span></span>

<span data-ttu-id="dbceb-114">Le tableau suivant montre la correspondance entre les services Azure existants et App Service, ainsi que les types d'applications qu'ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="dbceb-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="dbceb-115">Service Azure existant</span><span class="sxs-lookup"><span data-stu-id="dbceb-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="dbceb-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dbceb-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="dbceb-117">Ce qui a changé</span><span class="sxs-lookup"><span data-stu-id="dbceb-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="dbceb-118">Sites Web Azure</span><span class="sxs-lookup"><span data-stu-id="dbceb-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="dbceb-119">Applications Web</span><span class="sxs-lookup"><span data-stu-id="dbceb-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="dbceb-120">Pour Sites Web Azure, le changement concerne uniquement le remplacement du nom Sites Web en Applications web.</span><span class="sxs-lookup"><span data-stu-id="dbceb-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="dbceb-121">Toutes vos instances existantes de Sites Web s'appellent désormais Web Apps dans App Service.</span><span class="sxs-lookup"><span data-stu-id="dbceb-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="dbceb-122">Vous pouvez accéder à vos sites web existants via le <a href="http://go.microsoft.com/fwlink/?LinkId=529715">portail Azure</a>, où vous trouverez tous vos sites existants sous <em>Web Apps</em>.</span><span class="sxs-lookup"><span data-stu-id="dbceb-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="dbceb-123"><em>Web Plan d’hébergement</em> est désormais <em>du Plan App Service</em>.</span><span class="sxs-lookup"><span data-stu-id="dbceb-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="dbceb-124">Un <em>Plan App Service</em> peut héberger n’importe quel type d’application App Service (web, mobile, logique ou API).</span><span class="sxs-lookup"><span data-stu-id="dbceb-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="dbceb-125">Azure App Service Web Apps se trouve sous Disponibilité générale.</span><span class="sxs-lookup"><span data-stu-id="dbceb-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="dbceb-126"><a href="http://azure.microsoft.com/services/app-service/web/">En savoir plus sur les applications Web</a>.</span><span class="sxs-lookup"><span data-stu-id="dbceb-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="dbceb-127">Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="dbceb-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="dbceb-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="dbceb-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="dbceb-129">Mobile Services est toujours disponible en tant que service autonome et reste entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="dbceb-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="dbceb-130">Mobile Apps est un type d’application d’App Service qui intègre toutes les fonctionnalités de Mobile Services et plus encore.</span><span class="sxs-lookup"><span data-stu-id="dbceb-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="dbceb-131">La <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migration de Mobile Services à Mobile Apps</a> est facile.</span><span class="sxs-lookup"><span data-stu-id="dbceb-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="dbceb-132">Dans le cadre d’App Service, les applications mobiles se voient offrir de nouvelles fonctionnalités allant au-delà des services mobiles, comme l’intégration aux systèmes locaux et SaaS, les emplacements intermédiaires, WebJobs, de meilleures options de mise à l’échelle, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="dbceb-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="dbceb-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">En savoir plus sur les applications mobiles</a>.</span><span class="sxs-lookup"><span data-stu-id="dbceb-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="dbceb-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="dbceb-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="dbceb-135">API Apps est un nouveau type d'application d'App Service qui permet de créer et d'utiliser des API dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="dbceb-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="dbceb-136"><a href="http://azure.microsoft.com/services/app-service/api/">En savoir plus sur les applications API</a>.</span><span class="sxs-lookup"><span data-stu-id="dbceb-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="dbceb-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="dbceb-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="dbceb-138">Logic Apps est un nouveau type d’application d’App Service qui permet d’automatiser les processus d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="dbceb-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="dbceb-139"><a href="http://azure.microsoft.com/services/app-service/logic/">En savoir plus sur les applications de la logique de</a>.</span><span class="sxs-lookup"><span data-stu-id="dbceb-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="dbceb-140">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="dbceb-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="dbceb-141">Applications API BizTalk</span><span class="sxs-lookup"><span data-stu-id="dbceb-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="dbceb-142">BizTalk Services est toujours disponible en tant que service autonome et reste entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="dbceb-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="dbceb-143">Toutes les fonctionnalités de BizTalk Services sont intégrées à App Service en tant qu’applications API Apps permettant aux utilisateurs d’intégrer des applications d’entreprise et d’effectuer des intégrations B2B avec n’importe quel type d’application dans App Service.</span><span class="sxs-lookup"><span data-stu-id="dbceb-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="dbceb-144">Avec Logic Apps, vous pouvez désormais automatiser les processus d’entreprise grâce à une expérience de conception visuelle permettant de créer des flux de travail.</span><span class="sxs-lookup"><span data-stu-id="dbceb-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="dbceb-145">Pour plus d’informations, consultez la [documentation App Service](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="dbceb-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

