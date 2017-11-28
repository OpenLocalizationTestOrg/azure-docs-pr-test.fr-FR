---
title: "aaaMonitor contrôle d’intégrité et des alertes dans la pile de Azure | Documents Microsoft"
description: "Découvrez comment toomonitor contrôle d’intégrité et des alertes dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: chasat-MS
manager: dsavage
editor: 
ms.assetid: 69901c7b-4673-4bd8-acf2-8c6bdd9d1546
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: chasat
ms.openlocfilehash: 11e287c497e154b767c775fe4afcc78ec9e72fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a><span data-ttu-id="62759-103">Surveiller l’intégrité et les alertes dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="62759-103">Monitor health and alerts in Azure Stack</span></span>

<span data-ttu-id="62759-104">Pile Azure inclut des fonctionnalités qui permettent à un cloud opérateur tooview d’état et les alertes pour une région de la pile de Azure de surveillance de l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="62759-104">Azure Stack includes infrastructure monitoring capabilities that enable a cloud operator tooview health and alerts for an Azure Stack region.</span></span>

<span data-ttu-id="62759-105">Pile Azure possède un ensemble de fonctionnalités de gestion de la région disponibles Bonjour **gestion de la région** vignette.</span><span class="sxs-lookup"><span data-stu-id="62759-105">Azure Stack has a set of region management capabilities available in hello **Region management** tile.</span></span> <span data-ttu-id="62759-106">Cette vignette épinglée par défaut dans le portail d’administration hello pour hello abonnement du fournisseur par défaut, répertorie toutes les régions hello déployée de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="62759-106">This tile, pinned by default in hello administrator portal for hello Default Provider Subscription, lists all hello deployed regions of Azure Stack.</span></span> <span data-ttu-id="62759-107">Il montre également le nombre de hello des alertes actives critiques et d’avertissement pour chaque région.</span><span class="sxs-lookup"><span data-stu-id="62759-107">It also shows hello count of active critical and warning alerts for each region.</span></span> <span data-ttu-id="62759-108">Cette vignette est votre point d’entrée dans le contrôle d’intégrité hello et la fonctionnalité d’alerte de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="62759-108">This tile is your entry point into hello health and alert functionality of Azure Stack.</span></span>

 ![vignette de gestion de la région de Hello](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a><span data-ttu-id="62759-110">Présentation de l’intégrité dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="62759-110">Understand health in Azure Stack</span></span>

 <span data-ttu-id="62759-111">Contrôle d’intégrité et les alertes sont gérés dans la pile d’Azure par le fournisseur de ressources hello d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="62759-111">Health and alerts are managed in Azure Stack by hello Health resource provider.</span></span> <span data-ttu-id="62759-112">Composants d’infrastructure Azure pile inscrivent avec le fournisseur de ressources de contrôle d’intégrité hello lors du déploiement de la pile d’Azure et de configuration.</span><span class="sxs-lookup"><span data-stu-id="62759-112">Azure Stack infrastructure components register with hello Health resource provider during Azure Stack deployment and configuration.</span></span> <span data-ttu-id="62759-113">Cette inscription permet l’affichage hello de contrôle d’intégrité et les alertes pour chaque composant.</span><span class="sxs-lookup"><span data-stu-id="62759-113">This registration enables hello display of health and alerts for each component.</span></span> <span data-ttu-id="62759-114">L’intégrité dans Azure Stack est un concept simple.</span><span class="sxs-lookup"><span data-stu-id="62759-114">Health in Azure Stack is a simple concept.</span></span> <span data-ttu-id="62759-115">Si les alertes pour une instance enregistrée d’existent un composant, hello état d’intégrité de ce composant reflète hello pire active gravité d’alerte ; avertissement ou critique.</span><span class="sxs-lookup"><span data-stu-id="62759-115">If alerts for a registered instance of a component exist, hello health state of that component reflects hello worst active alert severity; warning, or critical.</span></span>
 
 ## <a name="view-and-manage-component-health-state"></a><span data-ttu-id="62759-116">Afficher et gérer l’état d’intégrité des composants</span><span class="sxs-lookup"><span data-stu-id="62759-116">View and manage component health state</span></span>
 
 <span data-ttu-id="62759-117">Vous pouvez afficher hello état des composants dans les deux portail d’administration Azure pile hello et via les API Rest et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62759-117">You can view hello health state of components in both hello Azure Stack administrator portal and through Rest API and PowerShell.</span></span>
 
<span data-ttu-id="62759-118">l’état d’intégrité tooview hello dans le portail hello, cliquez sur la région hello que vous souhaitez tooview Bonjour **gestion de la région** vignette.</span><span class="sxs-lookup"><span data-stu-id="62759-118">tooview hello health state in hello portal, click hello region that you want tooview in hello **Region management** tile.</span></span> <span data-ttu-id="62759-119">Vous pouvez afficher l’état d’intégrité hello de rôles d’infrastructure et des fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="62759-119">You can view hello health state of infrastructure roles and of resource providers.</span></span> <span data-ttu-id="62759-120">Notez que dans cette version, fournisseur de ressources de calcul hello ne signale pas l’état d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="62759-120">Note that in this release, hello Compute resource provider does not report health state.</span></span>

![Liste des rôles d’infrastructure](media/azure-stack-monitor-health/image2.png)

<span data-ttu-id="62759-122">Vous pouvez cliquer sur une ressource des tooview rôle fournisseur ou d’infrastructure des informations plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="62759-122">You can click a resource provider or infrastructure role tooview more detailed information.</span></span>

> [!WARNING]
><span data-ttu-id="62759-123">Si vous cliquez sur un rôle d’infrastructure, puis cliquez sur instance de rôle hello, il existe des options Bonjour **instance de rôle** panneau tooStart, redémarrage ou arrêt.</span><span class="sxs-lookup"><span data-stu-id="62759-123">If you click an infrastructure role, and then click hello role instance, there are options in hello **Role instance** blade tooStart, Restart, or Shutdown.</span></span> <span data-ttu-id="62759-124">N’utilisez **pas** ces options dans un environnement du Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="62759-124">Do **not** use these options in an Azure Stack Development Kit environment.</span></span> <span data-ttu-id="62759-125">Ces options sont conçues uniquement pour un environnement à plusieurs nœuds, où il existe plusieurs instances de rôle par rôle d’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="62759-125">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="62759-126">Le redémarrage d’une instance de rôle (notamment AzS Xrp01) dans le kit de développement hello provoque l’instabilité du système.</span><span class="sxs-lookup"><span data-stu-id="62759-126">Restarting a role instance (especially AzS-Xrp01) in hello development kit causes system instability.</span></span> <span data-ttu-id="62759-127">Pour la résolution des problèmes d’assistance, publiez votre toohello problème [Forum sur la pile de Azure](https://aka.ms/azurestackforum).</span><span class="sxs-lookup"><span data-stu-id="62759-127">For troubleshooting assistance, please post your issue toohello [Azure Stack forum](https://aka.ms/azurestackforum).</span></span>
>
 
## <a name="view-alerts"></a><span data-ttu-id="62759-128">Afficher les alertes</span><span class="sxs-lookup"><span data-stu-id="62759-128">View alerts</span></span>

<span data-ttu-id="62759-129">liste de Hello d’alertes actives pour chaque région de la pile de Azure est disponible directement à partir de hello **gestion de la région** panneau.</span><span class="sxs-lookup"><span data-stu-id="62759-129">hello list of active alerts for each Azure Stack region is available directly from hello **Region management** blade.</span></span> <span data-ttu-id="62759-130">première vignette dans la configuration par défaut de hello Hello est hello **alertes** vignette, qui affiche un résumé des alertes d’avertissement pour la région de hello hello critiques.</span><span class="sxs-lookup"><span data-stu-id="62759-130">hello first tile in hello default configuration is hello **Alerts** tile, which displays a summary of hello critical and warning alerts for hello region.</span></span> <span data-ttu-id="62759-131">Vous pouvez épingler la vignette d’alertes hello, comme n’importe quelle autre vignette sur ce panneau, toohello le tableau de bord pour un accès rapide.</span><span class="sxs-lookup"><span data-stu-id="62759-131">You can pin hello Alerts tile, like any other tile on this blade, toohello dashboard for quick access.</span></span>   

![Vignette Alertes qui affiche un avertissement](media/azure-stack-monitor-health/image3.png)

<span data-ttu-id="62759-133">En sélectionnant la partie supérieure de hello Hello **alertes** vignette, vous accédez liste toohello de toutes les alertes actives pour la région de hello.</span><span class="sxs-lookup"><span data-stu-id="62759-133">By selecting hello top portion of hello **Alerts** tile, you navigate toohello list of all active alerts for hello region.</span></span> <span data-ttu-id="62759-134">Si vous sélectionnez soit hello **critique** ou **avertissement** ligne de commande dans la vignette de hello, vous accédez tooa filtré la liste des alertes (critique ou avertissement).</span><span class="sxs-lookup"><span data-stu-id="62759-134">If you select either hello **Critical** or **Warning** line item within hello tile, you navigate tooa filtered list of alerts (Critical or Warning).</span></span> 

![Avertissements filtrés](media/azure-stack-monitor-health/image4.png)
  
<span data-ttu-id="62759-136">Hello **alertes** lame prend en charge hello capacité toofilter à la fois sur le niveau de gravité (critique ou avertissement) et l’état (actif ou fermé).</span><span class="sxs-lookup"><span data-stu-id="62759-136">hello **Alerts** blade supports hello ability toofilter both on status (Active or Closed) and severity (Critical or Warning).</span></span> <span data-ttu-id="62759-137">par défaut Hello affiche toutes les alertes actives.</span><span class="sxs-lookup"><span data-stu-id="62759-137">hello default view displays all Active alerts.</span></span> <span data-ttu-id="62759-138">Toutes les alertes fermées sont supprimés à partir du système de hello bout de sept jours.</span><span class="sxs-lookup"><span data-stu-id="62759-138">All closed alerts are removed from hello system after seven days.</span></span>

![Toofilter de volet de filtre en état critique ou d’avertissement](media/azure-stack-monitor-health/image5.png)

<span data-ttu-id="62759-140">panneau d’alertes Hello expose également hello **vue API** action, qui permet d’afficher le hello affiche les API Rest qui était la liste de hello toogenerate utilisé.</span><span class="sxs-lookup"><span data-stu-id="62759-140">hello Alerts blade also exposes hello **View API** action, which displays hello Rest API that was used toogenerate hello list view.</span></span> <span data-ttu-id="62759-141">Cette action fournit un moyen rapide de toobecome familiarisé avec la syntaxe d’API Rest hello que vous pouvez utiliser les alertes tooquery.</span><span class="sxs-lookup"><span data-stu-id="62759-141">This action provides a quick way toobecome familiar with hello Rest API syntax that you can use tooquery alerts.</span></span> <span data-ttu-id="62759-142">Vous pouvez utiliser cette API dans l’automation ou pour l’intégration avec vos solutions existantes de création de tickets, de création de rapports et de surveillance de centre de données.</span><span class="sxs-lookup"><span data-stu-id="62759-142">You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions.</span></span> 

![Hello option API de vue qui affiche hello API Rest](media/azure-stack-monitor-health/image6.png)

<span data-ttu-id="62759-144">À partir du panneau d’alertes hello, vous pouvez sélectionner un toohello alerte toonavigate **détails de l’alerte** panneau.</span><span class="sxs-lookup"><span data-stu-id="62759-144">From hello Alerts blade, you can select an alert toonavigate toohello **Alert details** blade.</span></span> <span data-ttu-id="62759-145">Ce panneau affiche tous les champs associés à l’alerte de hello, et permet une navigation rapide toohello affecté composant et source d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="62759-145">This blade displays all fields that are associated with hello alert, and enables quick navigation toohello affected component and source of hello alert.</span></span> <span data-ttu-id="62759-146">Par exemple, hello alerte suivante se produit si une des instances de rôle d’infrastructure hello est mis hors connexion ou n’est pas accessible.</span><span class="sxs-lookup"><span data-stu-id="62759-146">For example, hello following alert occurs if one of hello infrastructure role instances goes offline or is not accessible.</span></span>  

![Panneau de détails de l’alerte Hello](media/azure-stack-monitor-health/image7.png)

<span data-ttu-id="62759-148">Une fois l’instance de rôle d’infrastructure hello en ligne, cette alerte se ferme automatiquement.</span><span class="sxs-lookup"><span data-stu-id="62759-148">After hello infrastructure role instance is back online, this alert automatically closes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62759-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62759-149">Next steps</span></span>

[<span data-ttu-id="62759-150">Gérer les mises à jour dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="62759-150">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)

[<span data-ttu-id="62759-151">Gestion des régions dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="62759-151">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
