---
title: "stratégies de base lab aaaManage dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment tooset certaines des stratégies de base hello (paramètres) pour un atelier de DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="68706-103">Gérer les stratégies de laboratoire de base dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="68706-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="68706-104">Azure DevTest Labs vous toocontrol coût et réduire les pertes dans vos laboratoires grâce à la gestion des stratégies (paramètres) correspondant à chaque atelier.</span><span class="sxs-lookup"><span data-stu-id="68706-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="68706-105">Dans cet article, commencer à utiliser les stratégies par apprendre comment tooset deux des stratégies les plus critiques de hello - limitation hello nombre de machines virtuelles (VM) peut être créés ou demandés par un utilisateur unique et une configuration arrêt automatique.</span><span class="sxs-lookup"><span data-stu-id="68706-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="68706-106">tooview comment tooset chaque stratégie lab, consultez l’article hello, [définir des stratégies de lab dans Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="68706-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="68706-107">Accès aux stratégies d’un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="68706-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="68706-108">Hello étapes suivantes vous guident dans la configuration des stratégies pour un atelier de Azure DevTest Labs :</span><span class="sxs-lookup"><span data-stu-id="68706-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="68706-109">les stratégies hello tooview (et modifier) pour un laboratoire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="68706-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="68706-110">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="68706-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="68706-111">Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="68706-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="68706-112">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="68706-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="68706-113">Sélectionnez **Configuration et stratégies**.</span><span class="sxs-lookup"><span data-stu-id="68706-113">Select **Configuration and policies**.</span></span>

    ![Panneau Paramètres de stratégie](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="68706-115">Hello **stratégies de Configuration et** panneau contienne un menu des paramètres que vous pouvez spécifier.</span><span class="sxs-lookup"><span data-stu-id="68706-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="68706-116">Cet article traite uniquement les paramètres de hello pour **machines virtuelles par utilisateur** et **arrêt automatique**.</span><span class="sxs-lookup"><span data-stu-id="68706-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="68706-117">toolearn sur hello restant des paramètres, consultez [gérer toutes les stratégies pour un atelier de Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="68706-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="68706-118">Définir les machines virtuelles par utilisateur</span><span class="sxs-lookup"><span data-stu-id="68706-118">Set virtual machines per user</span></span>
<span data-ttu-id="68706-119">Hello stratégie pour **machines virtuelles par utilisateur** vous permet de toospecify hello nombre de machines virtuelles qui peuvent être créés par un utilisateur individuel.</span><span class="sxs-lookup"><span data-stu-id="68706-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="68706-120">Si un utilisateur tente de toocreate ou la revendication d’une machine virtuelle lors de la limite d’utilisateurs hello a été atteint, un message d’erreur indique que hello que machine virtuelle ne peut pas être créé/demandé.</span><span class="sxs-lookup"><span data-stu-id="68706-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="68706-121">Sur du laboratoire hello **stratégies de Configuration et** menu, sélectionnez **machines virtuelles par utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="68706-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Machines virtuelles par utilisateur](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="68706-123">Sélectionnez **Oui** toolimit hello plusieurs ordinateurs virtuels par utilisateur.</span><span class="sxs-lookup"><span data-stu-id="68706-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="68706-124">Si vous ne souhaitez pas toolimit hello plusieurs ordinateurs virtuels par utilisateur, sélectionnez **non**.</span><span class="sxs-lookup"><span data-stu-id="68706-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="68706-125">Si vous sélectionnez **Oui**, entrez une valeur numérique indiquant le nombre maximal de hello de machines virtuelles qui peuvent être créés ou demandé par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="68706-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="68706-126">Sélectionnez **Oui** nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD (SSD).</span><span class="sxs-lookup"><span data-stu-id="68706-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="68706-127">Si vous ne souhaitez pas le nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD, sélectionnez **non**.</span><span class="sxs-lookup"><span data-stu-id="68706-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="68706-128">Si vous sélectionnez **Oui**, entrez une valeur qui indique le nombre maximal de hello de machines virtuelles qui peuvent être créés à l’aide de disques SSD.</span><span class="sxs-lookup"><span data-stu-id="68706-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="68706-129">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="68706-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="68706-130">Définir l’arrêt automatique</span><span class="sxs-lookup"><span data-stu-id="68706-130">Set auto-shutdown</span></span>
<span data-ttu-id="68706-131">stratégie d’arrêt automatique Hello permet toominimize lab déchets, ce qui permet des temps de hello toospecify permettant d’arrêter des machines virtuelles de ce laboratoire.</span><span class="sxs-lookup"><span data-stu-id="68706-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="68706-132">Sur du laboratoire hello **stratégies de Configuration et** panneau, sélectionnez **arrêt automatique**.</span><span class="sxs-lookup"><span data-stu-id="68706-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Arrêt automatique](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="68706-134">Sélectionnez **sur** tooenable cette stratégie, et **hors** toodisable il.</span><span class="sxs-lookup"><span data-stu-id="68706-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="68706-135">Si vous activez cette stratégie, spécifiez tooshut de temps (et le fuseau horaire) hello tous les ordinateurs virtuels vers le bas dans le lab actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="68706-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="68706-136">Spécifiez **Oui** ou **non** pour hello option toosend un toohello préalable de 15 minutes de notification spécifié des temps d’arrêt automatique.</span><span class="sxs-lookup"><span data-stu-id="68706-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="68706-137">Si vous spécifiez **Oui**, entrez une notification de webhook URL du point de terminaison tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="68706-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="68706-138">Pour plus d’informations sur les webhooks, consultez [Créer une fonction Azure d’API ou de webhook](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="68706-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="68706-139">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="68706-139">Select **Save**.</span></span>

    <span data-ttu-id="68706-140">Par défaut, une fois activée, cette stratégie s’applique des machines virtuelles tooall pratiques hello.</span><span class="sxs-lookup"><span data-stu-id="68706-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="68706-141">tooremove ce paramètre à partir d’un ordinateur virtuel spécifique, ouvrir le panneau et la modification de la machine virtuelle hello son **arrêt automatique** paramètre</span><span class="sxs-lookup"><span data-stu-id="68706-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="68706-142">Définir le démarrage automatique</span><span class="sxs-lookup"><span data-stu-id="68706-142">Set auto-start</span></span>
<span data-ttu-id="68706-143">permet de stratégie de démarrage automatique Hello vous toospecify hello machines virtuelles dans le lab actuel de hello doit être démarré.</span><span class="sxs-lookup"><span data-stu-id="68706-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="68706-144">Sur du laboratoire hello **stratégies de Configuration et** panneau, sélectionnez **démarrage automatique**.</span><span class="sxs-lookup"><span data-stu-id="68706-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Démarrage automatique](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="68706-146">Sélectionnez **sur** tooenable cette stratégie, et **hors** toodisable il.</span><span class="sxs-lookup"><span data-stu-id="68706-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="68706-147">Si vous activez cette stratégie, spécifiez l’heure de début planifiée de hello, fuseau horaire et hello les jours de semaine hello pour le hello temps s’applique.</span><span class="sxs-lookup"><span data-stu-id="68706-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="68706-148">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="68706-148">Select **Save**.</span></span>

    <span data-ttu-id="68706-149">Une fois activée, cette stratégie n’est pas appliqué automatiquement tooany VM dans pratiques hello.</span><span class="sxs-lookup"><span data-stu-id="68706-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="68706-150">tooapply tooa de ce paramètre ordinateur virtuel spécifique, la machine virtuelle hello ouvrir Panneau et change son **démarrage automatique** paramètre</span><span class="sxs-lookup"><span data-stu-id="68706-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="68706-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68706-151">Next steps</span></span>

- <span data-ttu-id="68706-152">[Définir des stratégies de lab dans Azure DevTest Labs](devtest-lab-set-lab-policy.md) -en savoir comment toomodify autres stratégies de laboratoire</span><span class="sxs-lookup"><span data-stu-id="68706-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
