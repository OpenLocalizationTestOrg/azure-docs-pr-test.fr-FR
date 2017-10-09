---
title: "vue d’ensemble du contrôle d’intégrité de ressource aaaAzure | Documents Microsoft"
description: "Vue d’ensemble d’Azure Resource Health"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="bd5f3-103">Présentation d’Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="bd5f3-103">Azure resource health overview</span></span>
 
<span data-ttu-id="bd5f3-104">Resource Health vous permet d’établir des diagnostics et d’obtenir de l’aide lorsqu’un problème touchant Azure a des répercussions sur vos ressources.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="bd5f3-105">Il vous informe de la santé de vos ressources hello actuelles et passées et vous permet d’atténuer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="bd5f3-106">Resource Health propose un support technique dès lors que vous êtes confronté à des problèmes de service Azure et que vous avez besoin d’aide.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="bd5f3-107">Alors que [Azure Status](https://status.azure.com) vous informe des problèmes de service qui affectent un large éventail de clients Azure, l’intégrité des ressources vous offre un tableau de bord personnalisé d’intégrité hello de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="bd5f3-108">L’intégrité des ressources vous montre toutes les heures hello vos ressources n’étaient pas disponibles dans hello passé en raison de problèmes de service tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="bd5f3-109">Cela rend simple pour vous toounderstand si un contrat SLA a été violé.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="bd5f3-110">Qu’est-ce qu’une ressource et comment Resource Health juge-t-il de l’intégrité d’une ressource ?</span><span class="sxs-lookup"><span data-stu-id="bd5f3-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="bd5f3-111">Une ressource est une instance créée par un utilisateur d’un type de ressource fourni par un service Azure via Azure Resource Manager, par exemple une machine virtuelle, une application web ou une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="bd5f3-112">L’intégrité des ressources s’appuie sur des signaux émis par hello différents services Azure tooassess si une ressource est saine ou non.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="bd5f3-113">Si une ressource est défectueux, l’intégrité des ressources analyse les informations supplémentaires toodetermine hello source hello problème.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="bd5f3-114">Il identifie également les actions que Microsoft prend toofix hello problème ou faire ce qui les actions à entreprendre tooaddress hello provoquent de problème de hello.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="bd5f3-115">Révision hello la liste complète des types de ressources et d’intégrité vérifie [l’intégrité des ressources Azure](resource-health-checks-resource-types.md) pour plus d’informations sur la procédure d’évaluation d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="bd5f3-116">L’état d’intégrité fourni par Resource Health</span><span class="sxs-lookup"><span data-stu-id="bd5f3-116">Health status provided by resource health</span></span>
<span data-ttu-id="bd5f3-117">intégrité Hello d’une ressource est un des hello suivant des États :</span><span class="sxs-lookup"><span data-stu-id="bd5f3-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="bd5f3-118">Disponible</span><span class="sxs-lookup"><span data-stu-id="bd5f3-118">Available</span></span>
<span data-ttu-id="bd5f3-119">service de Hello n’a détecté que tous les événements ayant un impact sur l’intégrité de hello de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="bd5f3-120">Dans les cas où les ressources hello a récupéré de temps d’arrêt non planifié pendant hello dernières 24 heures, vous verrez hello **récemment récupéré** notification.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![Machine virtuelle disponible Resource Health](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="bd5f3-122">Non disponible</span><span class="sxs-lookup"><span data-stu-id="bd5f3-122">Unavailable</span></span>
<span data-ttu-id="bd5f3-123">service de Hello a détecté une plateforme en cours ou un événement non-plateforme ayant un impact sur l’intégrité de hello de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="bd5f3-124">Événements de plateforme</span><span class="sxs-lookup"><span data-stu-id="bd5f3-124">Platform events</span></span>
<span data-ttu-id="bd5f3-125">Ces événements sont déclenchés par plusieurs composants de hello infrastructure Azure et incluent les actions planifiées telles que de maintenance planifiée et des incidents inattendues comme un redémarrage de l’ordinateur hôte non planifié.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="bd5f3-126">L’intégrité des ressources fournit des détails supplémentaires sur l’événement hello, processus de récupération hello et vous permet la prise en charge de toocontact même si vous n’avez pas de contrat de support technique d’un Microsoft actif.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Ressource d’intégrité indisponible virtual machine en raison de l’événement de tooplatform](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="bd5f3-128">Événements hors plateforme</span><span class="sxs-lookup"><span data-stu-id="bd5f3-128">Non-Platform events</span></span>
<span data-ttu-id="bd5f3-129">Ces événements sont déclenchés par les actions effectuées par les utilisateurs, par exemple l’arrêt d’un ordinateur virtuel ou atteindre hello le nombre maximal de connexions tooa Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Ressource d’intégrité indisponible virtual machine en raison de l’événement de plate-forme de toonon](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="bd5f3-131">Unknown</span><span class="sxs-lookup"><span data-stu-id="bd5f3-131">Unknown</span></span>
<span data-ttu-id="bd5f3-132">L’état d’intégrité indique que Resource Health n’a reçu aucune information sur cette ressource depuis plus de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="bd5f3-133">Cet état n’est pas une indication définitive de l’état hello de ressource de hello, il est un point de données importantes dans hello processus de dépannage :</span><span class="sxs-lookup"><span data-stu-id="bd5f3-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="bd5f3-134">Si les ressources hello sont en cours d’exécution en tant qu’état hello attendu de ressource de hello met à jour tooAvailable après quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="bd5f3-135">Si vous rencontrez des problèmes avec les ressources hello, hello état d’intégrité inconnu peut suggérer la ressource de hello est affectée par un événement de plate-forme de hello.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![Machine virtuelle inconnue Resource Health](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="bd5f3-137">Signaler un état incorrect</span><span class="sxs-lookup"><span data-stu-id="bd5f3-137">Report an incorrect status</span></span>
<span data-ttu-id="bd5f3-138">Si à tout moment, vous pensez état d’intégrité actuel de hello est incorrect, vous pouvez faites-le nous savoir en cliquant sur **signaler l’état d’intégrité incorrect**.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="bd5f3-139">Dans les cas où vous n’êtes affecté à un problème d’Azure, nous vous encourageons prise en charge toocontact à partir du Panneau de contrôle d’intégrité des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![Signaler un état incorrect dans Resource Health](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="bd5f3-141">Informations d’historique</span><span class="sxs-lookup"><span data-stu-id="bd5f3-141">Historical Information</span></span>
<span data-ttu-id="bd5f3-142">Vous pouvez accéder à des jours too14 des données historiques d’intégrité en cliquant sur **afficher l’historique** dans le panneau de contrôle d’intégrité des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![Historique des rapports de Resource Health](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="bd5f3-144">Prise en main</span><span class="sxs-lookup"><span data-stu-id="bd5f3-144">Getting started</span></span>
<span data-ttu-id="bd5f3-145">tooopen l’intégrité des ressources pour une ressource</span><span class="sxs-lookup"><span data-stu-id="bd5f3-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="bd5f3-146">Connectez-vous en hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="bd5f3-147">Accédez tooyour ressource.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="bd5f3-148">Dans le menu de ressource hello situé dans la partie gauche hello, cliquez sur **l’intégrité des ressources**.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![Ouvrir Resource Health depuis le panneau Ressource](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="bd5f3-150">Vous pouvez également accéder à l’intégrité des ressources en cliquant sur **davantage de services**et en tapant **l’intégrité des ressources** Bonjour de tooopen de zone de texte filtre **aide et Support** panneau.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="bd5f3-151">Cliquez enfin sur [**Intégrité des ressources**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="bd5f3-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Ouvrir Resource Health depuis Plus de services](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="bd5f3-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd5f3-153">Next steps</span></span>

<span data-ttu-id="bd5f3-154">Passez en revue ces toolearn de ressources en savoir plus sur l’intégrité des ressources :</span><span class="sxs-lookup"><span data-stu-id="bd5f3-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="bd5f3-155">Types de ressources et les contrôles d’intégrité dans Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="bd5f3-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="bd5f3-156">Forum aux questions sur Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="bd5f3-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




