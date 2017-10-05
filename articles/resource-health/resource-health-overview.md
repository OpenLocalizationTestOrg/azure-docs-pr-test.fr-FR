---
title: "Présentation d’Azure Resource Health | Microsoft Docs"
description: "Vue d’ensemble d’Azure Resource Health"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: d54979995ca97a70ba92c64915b919da09f548ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="2f406-103">Présentation d’Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="2f406-103">Azure resource health overview</span></span>
 
<span data-ttu-id="2f406-104">Resource Health vous permet d’établir des diagnostics et d’obtenir de l’aide lorsqu’un problème touchant Azure a des répercussions sur vos ressources.</span><span class="sxs-lookup"><span data-stu-id="2f406-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="2f406-105">Il vous informe de l’intégrité (actuelle et passée) de vos ressources et vous aide à atténuer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="2f406-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="2f406-106">Resource Health propose un support technique dès lors que vous êtes confronté à des problèmes de service Azure et que vous avez besoin d’aide.</span><span class="sxs-lookup"><span data-stu-id="2f406-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="2f406-107">Là où le [Statut Azure](https://status.azure.com) vous informe des problèmes de service qui affectent un grand nombre de clients Azure, Resource Health vous offre un tableau de bord personnalisé de l’intégrité de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="2f406-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span></span> <span data-ttu-id="2f406-108">Resource Health vous montre toutes les fois où vos ressources ont été indisponibles dans le passé en raison de problèmes de service Azure.</span><span class="sxs-lookup"><span data-stu-id="2f406-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span></span> <span data-ttu-id="2f406-109">Cela vous permet de comprendre simplement si un contrat SLA a été enfreint.</span><span class="sxs-lookup"><span data-stu-id="2f406-109">This makes it simple for you to understand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="2f406-110">Qu’est-ce qu’une ressource et comment Resource Health juge-t-il de l’intégrité d’une ressource ?</span><span class="sxs-lookup"><span data-stu-id="2f406-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="2f406-111">Une ressource est une instance créée par un utilisateur d’un type de ressource fourni par un service Azure via Azure Resource Manager, par exemple une machine virtuelle, une application web ou une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2f406-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="2f406-112">Resource Health s’appuie sur des signaux émis par les différents services Azure pour évaluer l’intégrité d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="2f406-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span></span> <span data-ttu-id="2f406-113">Si une ressource n’est pas intègre, Resource Health analyse des informations supplémentaires pour déterminer la source du problème.</span><span class="sxs-lookup"><span data-stu-id="2f406-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span></span> <span data-ttu-id="2f406-114">Il identifie également les actions adoptées par Microsoft pour résoudre le problème ou les actions que vous pouvez prendre pour résoudre la cause du problème.</span><span class="sxs-lookup"><span data-stu-id="2f406-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span></span> 

<span data-ttu-id="2f406-115">Passez en revue la liste complète de types de ressource et de vérifications d’intégrité dans [Azure Resource Health](resource-health-checks-resource-types.md) pour plus d’informations sur la procédure d’évaluation de l’intégrité.</span><span class="sxs-lookup"><span data-stu-id="2f406-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="2f406-116">L’état d’intégrité fourni par Resource Health</span><span class="sxs-lookup"><span data-stu-id="2f406-116">Health status provided by resource health</span></span>
<span data-ttu-id="2f406-117">L’intégrité d’une ressource affiche un des états suivants :</span><span class="sxs-lookup"><span data-stu-id="2f406-117">The health of a resource is one of the following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="2f406-118">Disponible</span><span class="sxs-lookup"><span data-stu-id="2f406-118">Available</span></span>
<span data-ttu-id="2f406-119">Le service n’a pas détecté d’événements ayant un impact sur l’intégrité de la ressource.</span><span class="sxs-lookup"><span data-stu-id="2f406-119">The service has not detected any events impacting the health of the resource.</span></span> <span data-ttu-id="2f406-120">Dans les cas où la ressource a récupéré d’un arrêt non planifié au cours des dernières 24 heures, vous verrez la notification **récupération récente**.</span><span class="sxs-lookup"><span data-stu-id="2f406-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span></span>

![Machine virtuelle disponible Resource Health](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="2f406-122">Non disponible</span><span class="sxs-lookup"><span data-stu-id="2f406-122">Unavailable</span></span>
<span data-ttu-id="2f406-123">Le service a détecté un événement de plateforme ou hors plateforme en cours ayant un impact sur l’intégrité de la ressource.</span><span class="sxs-lookup"><span data-stu-id="2f406-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="2f406-124">Événements de plateforme</span><span class="sxs-lookup"><span data-stu-id="2f406-124">Platform events</span></span>
<span data-ttu-id="2f406-125">Ces événements sont déclenchés par plusieurs composants de l’infrastructure Azure et incluent les actions planifiées telles que de la maintenance planifiée, ainsi que les incidents inattendus, comme un redémarrage non planifié de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="2f406-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="2f406-126">Resource Health fournit des détails supplémentaires sur l’événement et le processus de récupération et vous permet de contacter le support technique même si vous n’avez pas un contrat de support technique Microsoft actif.</span><span class="sxs-lookup"><span data-stu-id="2f406-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span></span>

![Machine virtuelle indisponible Resource Health en raison d’un événement de plateforme](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="2f406-128">Événements hors plateforme</span><span class="sxs-lookup"><span data-stu-id="2f406-128">Non-Platform events</span></span>
<span data-ttu-id="2f406-129">Ces événements sont déclenchés par des actions effectuées par les utilisateurs, par exemple l’arrêt d’une machine virtuelle ou l’arrivée au nombre maximal de connexions à un cache Redis.</span><span class="sxs-lookup"><span data-stu-id="2f406-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span></span>

![Machine virtuelle indisponible Resource Health en raison d’un événement hors plateforme](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="2f406-131">Unknown</span><span class="sxs-lookup"><span data-stu-id="2f406-131">Unknown</span></span>
<span data-ttu-id="2f406-132">L’état d’intégrité indique que Resource Health n’a reçu aucune information sur cette ressource depuis plus de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="2f406-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="2f406-133">Si cet état n’est pas une indication définitive de l’état de la ressource, il s’agit d’un point de données important dans le processus de dépannage :</span><span class="sxs-lookup"><span data-stu-id="2f406-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span></span>
* <span data-ttu-id="2f406-134">Si la ressource fonctionne comme prévu, l’état de la ressource est mis à jour sur Disponible après quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="2f406-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span></span>
* <span data-ttu-id="2f406-135">Si vous rencontrez des problèmes avec la ressource, l’état d’intégrité Inconnu peut suggérer que la ressource est affectée par un événement dans la plateforme.</span><span class="sxs-lookup"><span data-stu-id="2f406-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span></span>

![Machine virtuelle inconnue Resource Health](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="2f406-137">Signaler un état incorrect</span><span class="sxs-lookup"><span data-stu-id="2f406-137">Report an incorrect status</span></span>
<span data-ttu-id="2f406-138">Si à tout moment, vous pensez que l’état actuel est incorrect, vous pouvez nous le faire savoir en cliquant sur **Signaler un état d’intégrité incorrect**.</span><span class="sxs-lookup"><span data-stu-id="2f406-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="2f406-139">Dans le cas où vous êtes affecté par un problème avec Azure, nous vous invitons à contacter le support à partir du panneau Resource Health.</span><span class="sxs-lookup"><span data-stu-id="2f406-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span></span> 

![Signaler un état incorrect dans Resource Health](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="2f406-141">Informations d’historique</span><span class="sxs-lookup"><span data-stu-id="2f406-141">Historical Information</span></span>
<span data-ttu-id="2f406-142">Vous pouvez accéder aux données historiques d’intégrité jusqu'à 14 jours en cliquant sur **Afficher l’historique** dans le panneau de Resource Health.</span><span class="sxs-lookup"><span data-stu-id="2f406-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span></span> 

![Historique des rapports de Resource Health](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="2f406-144">Prise en main</span><span class="sxs-lookup"><span data-stu-id="2f406-144">Getting started</span></span>
<span data-ttu-id="2f406-145">Pour ouvrir Resource Health pour une ressource</span><span class="sxs-lookup"><span data-stu-id="2f406-145">To open Resource health for one resource</span></span>
1.  <span data-ttu-id="2f406-146">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2f406-146">Sign in into the Azure portal.</span></span>
2.  <span data-ttu-id="2f406-147">Accédez à votre ressource.</span><span class="sxs-lookup"><span data-stu-id="2f406-147">Navigate to your resource.</span></span>
3.  <span data-ttu-id="2f406-148">Dans le menu de ressources situé dans la partie gauche, cliquez sur **Intégrité des ressources**.</span><span class="sxs-lookup"><span data-stu-id="2f406-148">In the resource menu located in the left-hand side, click **Resource health**.</span></span>

![Ouvrir Resource Health depuis le panneau Ressource](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="2f406-150">Vous pouvez également accéder à Resource Health en cliquant sur **Plus de services** et en saisissant **Resource Health** dans la zone de texte de filtre pour ouvrir le panneau **Aide + Support**.</span><span class="sxs-lookup"><span data-stu-id="2f406-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span></span> <span data-ttu-id="2f406-151">Cliquez enfin sur [**Intégrité des ressources**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="2f406-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Ouvrir Resource Health depuis Plus de services](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="2f406-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f406-153">Next steps</span></span>

<span data-ttu-id="2f406-154">Pour en savoir plus sur Resource Health, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f406-154">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="2f406-155">Types de ressources et les contrôles d’intégrité dans Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="2f406-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="2f406-156">Forum aux questions sur Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="2f406-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




