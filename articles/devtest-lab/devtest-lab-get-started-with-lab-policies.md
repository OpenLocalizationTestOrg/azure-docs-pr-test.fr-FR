---
title: "Gérer les stratégies de laboratoire de base dans Azure DevTest Labs | Microsoft Docs"
description: "Découvrez comment définir certaines des stratégies de base (paramètres) pour un laboratoire dans DevTest Labs"
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
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="1af6f-103">Gérer les stratégies de laboratoire de base dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1af6f-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="1af6f-104">Azure DevTest Labs vous permet de contrôler les coûts et de réduire le gaspillage dans vos laboratoires en gérant les stratégies (paramètres) de chacun d’entre eux.</span><span class="sxs-lookup"><span data-stu-id="1af6f-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="1af6f-105">Dans cet article, vous allez découvrir les stratégies en apprenant à définir deux d’entre elles parmi les plus critiques : la limitation du nombre de machines virtuelles pouvant être créées ou revendiquées par un seul utilisateur et la configuration de l’arrêt automatique.</span><span class="sxs-lookup"><span data-stu-id="1af6f-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="1af6f-106">Pour savoir comment définir chaque stratégie de laboratoire, consultez l’article [Définir des stratégies de laboratoire dans Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1af6f-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="1af6f-107">Accès aux stratégies d’un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1af6f-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="1af6f-108">Les étapes suivantes vous guident lors de la configuration des stratégies pour un laboratoire dans Azure DevTest Labs :</span><span class="sxs-lookup"><span data-stu-id="1af6f-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="1af6f-109">Pour afficher (et modifier) les stratégies d’un laboratoire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1af6f-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="1af6f-110">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="1af6f-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="1af6f-111">Sélectionnez **Plus de services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="1af6f-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="1af6f-112">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="1af6f-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="1af6f-113">Sélectionnez **Configuration et stratégies**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-113">Select **Configuration and policies**.</span></span>

    ![Panneau Paramètres de stratégie](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="1af6f-115">Le panneau **Configuration et stratégies** contient un menu de paramètres que vous pouvez spécifier.</span><span class="sxs-lookup"><span data-stu-id="1af6f-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="1af6f-116">Cet article traite uniquement des paramètres concernant les **machines virtuelles par utilisateur** et **l’arrêt automatique**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="1af6f-117">Pour en savoir plus sur les autres paramètres, consultez [Gérer toutes les stratégies de laboratoire dans Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1af6f-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="1af6f-118">Définir les machines virtuelles par utilisateur</span><span class="sxs-lookup"><span data-stu-id="1af6f-118">Set virtual machines per user</span></span>
<span data-ttu-id="1af6f-119">La stratégie **Machines virtuelles par utilisateur** vous permet de spécifier le nombre maximal de machines virtuelles pouvant être créées par un utilisateur individuel.</span><span class="sxs-lookup"><span data-stu-id="1af6f-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="1af6f-120">Si un utilisateur tente de créer ou de revendiquer une machine virtuelle alors que le nombre limite par utilisateur est atteint, un message d’erreur indique que la machine virtuelle ne peut pas être créée/revendiquée.</span><span class="sxs-lookup"><span data-stu-id="1af6f-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="1af6f-121">Dans le menu **Configuration et stratégies** du laboratoire, sélectionnez **Machines virtuelles par utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Machines virtuelles par utilisateur](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="1af6f-123">Sélectionnez **Oui** pour limiter le nombre de machines virtuelles par utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1af6f-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="1af6f-124">Si vous ne souhaitez pas limiter le nombre de machines virtuelles par utilisateur, sélectionnez **Non**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="1af6f-125">Si vous sélectionnez **Oui**, entrez une valeur numérique indiquant le nombre maximal de machines virtuelles qu’un utilisateur peut créer ou revendiquer.</span><span class="sxs-lookup"><span data-stu-id="1af6f-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="1af6f-126">Sélectionnez **Oui** pour limiter le nombre de machines virtuelles pouvant utiliser un disque SSD.</span><span class="sxs-lookup"><span data-stu-id="1af6f-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="1af6f-127">Si vous ne souhaitez pas limiter le nombre de machines virtuelles pouvant utiliser un disque SSD, sélectionnez **Non**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="1af6f-128">Si vous sélectionnez **Oui**, entrez une valeur indiquant le nombre maximal de machines virtuelles qu’un utilisateur peut créer à l’aide d’un disque SSD.</span><span class="sxs-lookup"><span data-stu-id="1af6f-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="1af6f-129">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="1af6f-130">Définir l’arrêt automatique</span><span class="sxs-lookup"><span data-stu-id="1af6f-130">Set auto-shutdown</span></span>
<span data-ttu-id="1af6f-131">La stratégie d’arrêt automatique vous permet d’indiquer l’heure à laquelle les machines virtuelles du laboratoire doivent s’arrêter et contribue ainsi à réduire les pertes de laboratoire.</span><span class="sxs-lookup"><span data-stu-id="1af6f-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="1af6f-132">Dans le panneau **Configuration et stratégies**, sélectionnez **Arrêt automatique**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Arrêt automatique](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="1af6f-134">Sélectionnez **Activer** ou **Désactiver** pour activer ou désactiver cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="1af6f-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="1af6f-135">Si vous activez cette stratégie, spécifiez l’heure (et le fuseau horaire) de l’arrêt pour toutes les machines virtuelles du laboratoire actif.</span><span class="sxs-lookup"><span data-stu-id="1af6f-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="1af6f-136">Spécifiez **Oui** ou **Non** pour l’option d’envoi de notification 15 minutes avant l’heure d’arrêt automatique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="1af6f-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="1af6f-137">Si vous spécifiez **Oui**, entrez un point de terminaison d’URL webhook pour recevoir la notification.</span><span class="sxs-lookup"><span data-stu-id="1af6f-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="1af6f-138">Pour plus d’informations sur les webhooks, consultez [Créer une fonction Azure d’API ou de webhook](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="1af6f-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="1af6f-139">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-139">Select **Save**.</span></span>

    <span data-ttu-id="1af6f-140">Par défaut, une fois activée, cette stratégie s’applique à toutes les machines virtuelles dans le laboratoire en cours.</span><span class="sxs-lookup"><span data-stu-id="1af6f-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="1af6f-141">Pour supprimer ce paramètre sur une machine virtuelle spécifique, ouvrez le panneau de la machine virtuelle et modifiez son paramètre **Arrêt automatique** .</span><span class="sxs-lookup"><span data-stu-id="1af6f-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="1af6f-142">Définir le démarrage automatique</span><span class="sxs-lookup"><span data-stu-id="1af6f-142">Set auto-start</span></span>
<span data-ttu-id="1af6f-143">La stratégie de démarrage automatique vous permet de spécifier quand les machines virtuelles du laboratoire doivent être démarrées.</span><span class="sxs-lookup"><span data-stu-id="1af6f-143">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="1af6f-144">Dans le panneau **Configuration et stratégies**, sélectionnez **Démarrage automatique**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-144">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Démarrage automatique](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="1af6f-146">Sélectionnez **Activer** ou **Désactiver** pour activer ou désactiver cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="1af6f-146">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="1af6f-147">Si vous activez cette stratégie, spécifiez l’heure de démarrage programmée, le fuseau horaire et les jours de la semaine auxquels cette heure s’applique.</span><span class="sxs-lookup"><span data-stu-id="1af6f-147">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="1af6f-148">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1af6f-148">Select **Save**.</span></span>

    <span data-ttu-id="1af6f-149">Une fois activée, cette stratégie n’est pas automatiquement appliquée à toutes les machines virtuelles dans le laboratoire en cours.</span><span class="sxs-lookup"><span data-stu-id="1af6f-149">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="1af6f-150">Pour appliquer ce paramètre à une machine virtuelle spécifique, ouvrez le panneau de la machine virtuelle et modifiez son paramètre **Démarrage automatique** .</span><span class="sxs-lookup"><span data-stu-id="1af6f-150">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1af6f-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1af6f-151">Next steps</span></span>

- <span data-ttu-id="1af6f-152">[Définir des stratégies de laboratoire dans Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Apprenez à modifier les autres stratégies de laboratoire</span><span class="sxs-lookup"><span data-stu-id="1af6f-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 
