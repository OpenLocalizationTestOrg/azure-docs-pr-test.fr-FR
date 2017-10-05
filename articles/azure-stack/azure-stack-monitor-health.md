---
title: "Surveiller l’intégrité et les alertes dans Azure Stack | Microsoft Docs"
description: "Découvrez comment surveiller l’intégrité et les alertes dans Azure Stack."
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
ms.openlocfilehash: 93835eabcf9622735aada0f5dfa46028553c25bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a><span data-ttu-id="df557-103">Surveiller l’intégrité et les alertes dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="df557-103">Monitor health and alerts in Azure Stack</span></span>

<span data-ttu-id="df557-104">Azure Stack inclut des fonctionnalités de surveillance de l’infrastructure qui permettent à un opérateur cloud de visualiser les alertes et l’intégrité d’une région Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="df557-104">Azure Stack includes infrastructure monitoring capabilities that enable a cloud operator to view health and alerts for an Azure Stack region.</span></span>

<span data-ttu-id="df557-105">Azure Stack dispose d’un ensemble de fonctionnalités de gestion des régions disponibles dans la vignette **Gestion des régions**.</span><span class="sxs-lookup"><span data-stu-id="df557-105">Azure Stack has a set of region management capabilities available in the **Region management** tile.</span></span> <span data-ttu-id="df557-106">Cette vignette, épinglée par défaut dans le portail administrateur de l’abonnement Fournisseur par défaut, répertorie toutes les régions déployées d’Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="df557-106">This tile, pinned by default in the administrator portal for the Default Provider Subscription, lists all the deployed regions of Azure Stack.</span></span> <span data-ttu-id="df557-107">Elle montre également le nombre d’alertes critiques et d’avertissement actifs pour chaque région.</span><span class="sxs-lookup"><span data-stu-id="df557-107">It also shows the count of active critical and warning alerts for each region.</span></span> <span data-ttu-id="df557-108">Cette vignette est votre point d’entrée vers la fonctionnalité d’alerte et d’intégrité d’Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="df557-108">This tile is your entry point into the health and alert functionality of Azure Stack.</span></span>

 ![Vignette Gestion des régions](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a><span data-ttu-id="df557-110">Présentation de l’intégrité dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="df557-110">Understand health in Azure Stack</span></span>

 <span data-ttu-id="df557-111">L’intégrité et les alertes sont gérées dans Azure Stack par le fournisseur de ressources Intégrité.</span><span class="sxs-lookup"><span data-stu-id="df557-111">Health and alerts are managed in Azure Stack by the Health resource provider.</span></span> <span data-ttu-id="df557-112">Les composants d’infrastructure Azure Stack s’inscrivent auprès du fournisseur de ressources Intégrité lors du déploiement et de la configuration d’Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="df557-112">Azure Stack infrastructure components register with the Health resource provider during Azure Stack deployment and configuration.</span></span> <span data-ttu-id="df557-113">Cette inscription permet de visualiser l’intégrité et les alertes pour chaque composant.</span><span class="sxs-lookup"><span data-stu-id="df557-113">This registration enables the display of health and alerts for each component.</span></span> <span data-ttu-id="df557-114">L’intégrité dans Azure Stack est un concept simple.</span><span class="sxs-lookup"><span data-stu-id="df557-114">Health in Azure Stack is a simple concept.</span></span> <span data-ttu-id="df557-115">S’il existe des alertes pour une instance inscrite d’un composant, l’état d’intégrité de ce composant reflète la gravité de l’alerte active la plus sévère : avertissement ou critique.</span><span class="sxs-lookup"><span data-stu-id="df557-115">If alerts for a registered instance of a component exist, the health state of that component reflects the worst active alert severity; warning, or critical.</span></span>
 
 ## <a name="view-and-manage-component-health-state"></a><span data-ttu-id="df557-116">Afficher et gérer l’état d’intégrité des composants</span><span class="sxs-lookup"><span data-stu-id="df557-116">View and manage component health state</span></span>
 
 <span data-ttu-id="df557-117">Vous pouvez afficher l’état d’intégrité des composants dans le portail administrateur d’Azure Stack et par le biais des API Rest et de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df557-117">You can view the health state of components in both the Azure Stack administrator portal and through Rest API and PowerShell.</span></span>
 
<span data-ttu-id="df557-118">Pour afficher l’état d’intégrité dans le portail, cliquez sur la région que vous souhaitez visualiser dans la vignette **Gestion des régions**.</span><span class="sxs-lookup"><span data-stu-id="df557-118">To view the health state in the portal, click the region that you want to view in the **Region management** tile.</span></span> <span data-ttu-id="df557-119">Vous pouvez afficher l’état d’intégrité des rôles d’infrastructure et des fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="df557-119">You can view the health state of infrastructure roles and of resource providers.</span></span> <span data-ttu-id="df557-120">Notez que dans cette version, le fournisseur de ressources Calcul ne signale pas l’état d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="df557-120">Note that in this release, the Compute resource provider does not report health state.</span></span>

![Liste des rôles d’infrastructure](media/azure-stack-monitor-health/image2.png)

<span data-ttu-id="df557-122">Vous pouvez cliquer sur un fournisseur de ressources ou un rôle d’infrastructure pour afficher des informations plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="df557-122">You can click a resource provider or infrastructure role to view more detailed information.</span></span>

> [!WARNING]
><span data-ttu-id="df557-123">Si vous cliquez sur un rôle d’infrastructure puis sur l’instance de rôle, des options Démarrer, Redémarrer ou Arrêter s’affichent dans le panneau **Instance de rôle**.</span><span class="sxs-lookup"><span data-stu-id="df557-123">If you click an infrastructure role, and then click the role instance, there are options in the **Role instance** blade to Start, Restart, or Shutdown.</span></span> <span data-ttu-id="df557-124">N’utilisez **pas** ces options dans un environnement du Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="df557-124">Do **not** use these options in an Azure Stack Development Kit environment.</span></span> <span data-ttu-id="df557-125">Elles sont conçues uniquement pour un environnement à plusieurs nœuds, où il existe plusieurs instances de rôle par rôle d’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="df557-125">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="df557-126">Le redémarrage d’une instance de rôle (notamment AzS-Xrp01) dans le Kit de développement entraîne une instabilité du système.</span><span class="sxs-lookup"><span data-stu-id="df557-126">Restarting a role instance (especially AzS-Xrp01) in the development kit causes system instability.</span></span> <span data-ttu-id="df557-127">Pour obtenir une assistance en cas de problème, postez votre problème sur le [Forum Azure Stack](https://aka.ms/azurestackforum).</span><span class="sxs-lookup"><span data-stu-id="df557-127">For troubleshooting assistance, please post your issue to the [Azure Stack forum](https://aka.ms/azurestackforum).</span></span>
>
 
## <a name="view-alerts"></a><span data-ttu-id="df557-128">Afficher les alertes</span><span class="sxs-lookup"><span data-stu-id="df557-128">View alerts</span></span>

<span data-ttu-id="df557-129">La liste des alertes actives pour chaque région Azure Stack est disponible directement à partir du panneau **Gestion des régions**.</span><span class="sxs-lookup"><span data-stu-id="df557-129">The list of active alerts for each Azure Stack region is available directly from the **Region management** blade.</span></span> <span data-ttu-id="df557-130">La première vignette dans la configuration par défaut est la vignette **Alertes**, qui fournit un récapitulatif des alertes critiques et des avertissements pour la région.</span><span class="sxs-lookup"><span data-stu-id="df557-130">The first tile in the default configuration is the **Alerts** tile, which displays a summary of the critical and warning alerts for the region.</span></span> <span data-ttu-id="df557-131">Vous pouvez épingler la vignette Alertes au tableau de bord (comme n’importe quelle autre vignette sur ce panneau) pour pouvoir y accéder rapidement.</span><span class="sxs-lookup"><span data-stu-id="df557-131">You can pin the Alerts tile, like any other tile on this blade, to the dashboard for quick access.</span></span>   

![Vignette Alertes qui affiche un avertissement](media/azure-stack-monitor-health/image3.png)

<span data-ttu-id="df557-133">En sélectionnant la partie supérieure de la vignette **Alertes**, vous accédez à la liste de toutes les alertes actives pour la région.</span><span class="sxs-lookup"><span data-stu-id="df557-133">By selecting the top portion of the **Alerts** tile, you navigate to the list of all active alerts for the region.</span></span> <span data-ttu-id="df557-134">Si vous sélectionnez l’élément de ligne **Critique** ou **Avertissement** dans la vignette, vous accédez à une liste filtrée des alertes (Critique ou Avertissement).</span><span class="sxs-lookup"><span data-stu-id="df557-134">If you select either the **Critical** or **Warning** line item within the tile, you navigate to a filtered list of alerts (Critical or Warning).</span></span> 

![Avertissements filtrés](media/azure-stack-monitor-health/image4.png)
  
<span data-ttu-id="df557-136">Le panneau **Alertes** prend en charge la possibilité de filtrer à la fois sur le niveau de gravité (Critique ou Avertissement) et sur l’état (Actif ou Fermé).</span><span class="sxs-lookup"><span data-stu-id="df557-136">The **Alerts** blade supports the ability to filter both on status (Active or Closed) and severity (Critical or Warning).</span></span> <span data-ttu-id="df557-137">L’affichage par défaut montre toutes les alertes actives.</span><span class="sxs-lookup"><span data-stu-id="df557-137">The default view displays all Active alerts.</span></span> <span data-ttu-id="df557-138">Toutes les alertes fermées sont supprimées du système après sept jours.</span><span class="sxs-lookup"><span data-stu-id="df557-138">All closed alerts are removed from the system after seven days.</span></span>

![Volet Filtre pour filtrer par état Critique ou Avertissement](media/azure-stack-monitor-health/image5.png)

<span data-ttu-id="df557-140">Le panneau Alertes expose également l’action **API de vue**, qui montre l’API Rest utilisée pour générer la vue de liste.</span><span class="sxs-lookup"><span data-stu-id="df557-140">The Alerts blade also exposes the **View API** action, which displays the Rest API that was used to generate the list view.</span></span> <span data-ttu-id="df557-141">Cette action permet de se familiariser rapidement avec la syntaxe d’API Rest que vous pouvez utiliser pour interroger les alertes.</span><span class="sxs-lookup"><span data-stu-id="df557-141">This action provides a quick way to become familiar with the Rest API syntax that you can use to query alerts.</span></span> <span data-ttu-id="df557-142">Vous pouvez utiliser cette API dans l’automation ou pour l’intégration avec vos solutions existantes de création de tickets, de création de rapports et de surveillance de centre de données.</span><span class="sxs-lookup"><span data-stu-id="df557-142">You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions.</span></span> 

![L’option API de vue qui montre l’API Rest](media/azure-stack-monitor-health/image6.png)

<span data-ttu-id="df557-144">Dans le panneau Alertes, vous pouvez sélectionner une alerte pour accéder au panneau **Détails de l’alerte**.</span><span class="sxs-lookup"><span data-stu-id="df557-144">From the Alerts blade, you can select an alert to navigate to the **Alert details** blade.</span></span> <span data-ttu-id="df557-145">Ce panneau affiche tous les champs associés à l’alerte, et permet d’accéder rapidement au composant affecté et à la source de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="df557-145">This blade displays all fields that are associated with the alert, and enables quick navigation to the affected component and source of the alert.</span></span> <span data-ttu-id="df557-146">Par exemple, l’alerte suivante se produit si l’une des instances de rôle d’infrastructure bascule hors connexion ou est inaccessible.</span><span class="sxs-lookup"><span data-stu-id="df557-146">For example, the following alert occurs if one of the infrastructure role instances goes offline or is not accessible.</span></span>  

![Le panneau Détails de l’alerte](media/azure-stack-monitor-health/image7.png)

<span data-ttu-id="df557-148">Une fois l’instance de rôle d’infrastructure de nouveau en ligne, cette alerte se ferme automatiquement.</span><span class="sxs-lookup"><span data-stu-id="df557-148">After the infrastructure role instance is back online, this alert automatically closes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df557-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df557-149">Next steps</span></span>

[<span data-ttu-id="df557-150">Gérer les mises à jour dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="df557-150">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)

[<span data-ttu-id="df557-151">Gestion des régions dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="df557-151">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
