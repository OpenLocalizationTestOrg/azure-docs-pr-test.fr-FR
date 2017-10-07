---
title: gestion des aaaRegion dans la pile de Azure | Documents Microsoft
description: "Vue d’ensemble de la gestion des régions dans Azure Stack."
services: azure-stack
documentationcenter: 
author: efemmano
manager: dsavage
editor: 
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: efemmano
ms.openlocfilehash: c20fed831267aaf0447925ac261d7ee3f235c96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="region-management-in-azure-stack"></a><span data-ttu-id="41aa5-103">Gestion des régions dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="41aa5-103">Region management in Azure Stack</span></span>
<span data-ttu-id="41aa5-104">Pile Azure a un concept hello de régions, qui sont des entités logiques constituées des ressources matérielles hello qui composent hello Azure pile infrastructure.</span><span class="sxs-lookup"><span data-stu-id="41aa5-104">Azure Stack has hello concept of regions, which are logical entities comprised of hello hardware resources that make up hello Azure Stack infrastructure.</span></span> <span data-ttu-id="41aa5-105">À l’intérieur de gestion de la région, vous pouvez rechercher toutes les ressources qui sont requis toosuccessfully fonctionnent infrastructure du cycle de vie Azure pile hello.</span><span class="sxs-lookup"><span data-stu-id="41aa5-105">Inside Region management, you can find all resources that are required toosuccessfully operate hello Azure Stack infrastructure lifecycle.</span></span>

<span data-ttu-id="41aa5-106">Bonjour Kit de développement de pile Azure est un déploiement à nœud unique et est égal à une région.</span><span class="sxs-lookup"><span data-stu-id="41aa5-106">hello Azure Stack Development Kit is a single-node deployment, and equals one region.</span></span> <span data-ttu-id="41aa5-107">Si vous configurez une autre instance de hello Kit de développement de pile Azure sur un ordinateur distinct, cette instance est une autre région.</span><span class="sxs-lookup"><span data-stu-id="41aa5-107">If you set up another instance of hello Azure Stack Development Kit on separate hardware, this instance is a different region.</span></span>

## <a name="information-available-through-hello-region-management-tile"></a><span data-ttu-id="41aa5-108">Informations disponibles via la vignette de gestion de la région de hello</span><span class="sxs-lookup"><span data-stu-id="41aa5-108">Information available through hello Region Management tile</span></span>
<span data-ttu-id="41aa5-109">Pile Azure possède un ensemble de fonctionnalités de gestion de la région disponibles Bonjour **gestion de la région** vignette.</span><span class="sxs-lookup"><span data-stu-id="41aa5-109">Azure Stack has a set of region management capabilities available in hello **Region management** tile.</span></span> <span data-ttu-id="41aa5-110">Cette vignette est l’administrateur du cloud tooa disponible sur le tableau de bord hello par défaut dans le portail d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="41aa5-110">This tile is available tooa cloud administrator on hello default dashboard in hello administrator portal.</span></span> <span data-ttu-id="41aa5-111">Elle vous permet de surveiller et de mettre à jour votre région Azure Stack et ses composants, qui sont propres à la région.</span><span class="sxs-lookup"><span data-stu-id="41aa5-111">Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.</span></span>

 ![vignette de gestion de la région de Hello](media/azure-stack-manage-region/image1.png)

 <span data-ttu-id="41aa5-113">Si vous cliquez sur une région de la vignette de gestion de la région de hello, vous pouvez accéder hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="41aa5-113">If you click a region in hello Region management tile, you can access hello following information:</span></span>

  ![Description des volets dans le panneau de gestion de la région de hello](media/azure-stack-manage-region/image2.png)

1. <span data-ttu-id="41aa5-115">**menu de ressource Hello**.</span><span class="sxs-lookup"><span data-stu-id="41aa5-115">**hello resource menu**.</span></span> <span data-ttu-id="41aa5-116">Ici, vous pouvez accéder à des zones de gestion de l’infrastructure spécifiques, ainsi qu’afficher et gérer des ressources locataire telles que des comptes de stockage et des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="41aa5-116">Here, you can access specific infrastructure management areas, and view and manage tenant resources such as storage accounts and virtual networks.</span></span>

2. <span data-ttu-id="41aa5-117">**Alertes**.</span><span class="sxs-lookup"><span data-stu-id="41aa5-117">**Alerts**.</span></span> <span data-ttu-id="41aa5-118">Cette vignette répertorie les alertes à l’échelle du système et fournit des détails sur chacune de ces alertes.</span><span class="sxs-lookup"><span data-stu-id="41aa5-118">This tile lists system-wide alerts and provides details on each of those alerts.</span></span>

3. <span data-ttu-id="41aa5-119">**Mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="41aa5-119">**Updates**.</span></span> <span data-ttu-id="41aa5-120">Dans cette vignette, vous pouvez afficher la version actuelle de hello de votre infrastructure de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="41aa5-120">In this tile, you can view hello current version of your Azure Stack infrastructure.</span></span>

4. <span data-ttu-id="41aa5-121">**Fournisseurs de ressources**.</span><span class="sxs-lookup"><span data-stu-id="41aa5-121">**Resource providers**.</span></span> <span data-ttu-id="41aa5-122">Fournisseurs de ressources est hello place toomanage hello client les fonctionnalités offertes par hello composants toorun requis Azure pile.</span><span class="sxs-lookup"><span data-stu-id="41aa5-122">Resource providers is hello place toomanage hello tenant functionality offered by hello components required toorun Azure Stack.</span></span> <span data-ttu-id="41aa5-123">Chaque fournisseur de ressources est fourni avec une expérience d’administration.</span><span class="sxs-lookup"><span data-stu-id="41aa5-123">Each resource provider comes with an administrative experience.</span></span> <span data-ttu-id="41aa5-124">Cette expérience peut inclure des alertes pour un fournisseur spécifique de hello, métriques et autre fournisseur de ressources de gestion des capacités toohello spécifique.</span><span class="sxs-lookup"><span data-stu-id="41aa5-124">This experience can include alerts for hello specific provider, metrics, and other management capabilities specific toohello resource provider.</span></span>
 
5. <span data-ttu-id="41aa5-125">**Rôles d’infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="41aa5-125">**Infrastructure roles**.</span></span> <span data-ttu-id="41aa5-126">Rôles d’infrastructure sont hello composants toorun nécessaire Azure pile.</span><span class="sxs-lookup"><span data-stu-id="41aa5-126">Infrastructure roles are hello components necessary toorun Azure Stack.</span></span> <span data-ttu-id="41aa5-127">Rôles d’infrastructure hello uniquement qui signalent des alertes sont répertoriées.</span><span class="sxs-lookup"><span data-stu-id="41aa5-127">Only hello infrastructure roles that report alerts are listed.</span></span> <span data-ttu-id="41aa5-128">En cliquant sur un rôle, vous pouvez afficher les alertes de hello associés de rôle spécifique de hello et instances de rôle hello où ce rôle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="41aa5-128">By clicking a role, you can view hello alerts associated with hello specific role and hello role instances where this role is running.</span></span> <span data-ttu-id="41aa5-129">Bien que hello fonctionnalité toostart, redémarrer, ou arrêter une instance de rôle d’infrastructure, procédez comme **pas** cela dans un environnement de kit de développement.</span><span class="sxs-lookup"><span data-stu-id="41aa5-129">Although there is hello capability toostart, restart, or shut down an infrastructure role instance, do **not** do this in a development kit environment.</span></span> <span data-ttu-id="41aa5-130">Ces options sont conçues uniquement pour un environnement à plusieurs nœuds, où il existe plusieurs instances de rôle par rôle d’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="41aa5-130">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="41aa5-131">Le redémarrage d’une instance de rôle (notamment AzS Xrp01) dans le kit de développement hello provoque l’instabilité du système.</span><span class="sxs-lookup"><span data-stu-id="41aa5-131">Restarting a role instance (especially AzS-Xrp01) in hello development kit causes system instability.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41aa5-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41aa5-132">Next steps</span></span>
[<span data-ttu-id="41aa5-133">Surveiller l’intégrité et les alertes dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="41aa5-133">Monitor health and alerts in Azure Stack</span></span>](azure-stack-monitor-health.md)

[<span data-ttu-id="41aa5-134">Gérer les mises à jour dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="41aa5-134">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)






