---
title: "Gérer les stratégies de laboratoire dans Azure DevTest Labs | Microsoft Docs"
description: "Apprenez à définir des stratégies de laboratoire telles que les tailles de machine virtuelle, le nombre maximal de machines virtuelles par utilisateur et l’arrêt automatique."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 328a4d893637d7150807855e118b485a2c3bbfc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="b1e77-103">Gérer toutes les stratégies d’un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b1e77-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="b1e77-104">Azure DevTest Labs vous permet de contrôler les coûts et de réduire le gaspillage dans vos laboratoires en gérant les stratégies (paramètres) de chacun d’entre eux.</span><span class="sxs-lookup"><span data-stu-id="b1e77-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="b1e77-105">Cet article décrit étape par étape comment définir chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="b1e77-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="b1e77-106">Définir les tailles de machine virtuelle autorisées</span><span class="sxs-lookup"><span data-stu-id="b1e77-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="b1e77-107">La stratégie pour définir les tailles de machine virtuelle autorisées vous permet de spécifier les tailles de machine virtuelle autorisées dans le laboratoire et contribue ainsi à réduire les pertes de laboratoire.</span><span class="sxs-lookup"><span data-stu-id="b1e77-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="b1e77-108">Si cette stratégie est activée, seules les tailles de machine virtuelle de cette liste peuvent être utilisées pour créer des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b1e77-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="b1e77-109">Dans le panneau **Configuration et stratégies** du laboratoire, sélectionnez **Tailles de machine virtuelle autorisées**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Tailles de machine virtuelle autorisées](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="b1e77-111">Sélectionnez **Activer** ou **Désactiver** pour activer ou désactiver cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="b1e77-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="b1e77-112">Si vous activez cette stratégie, sélectionnez une ou plusieurs tailles de machine virtuelle pouvant être créées dans votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="b1e77-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="b1e77-113">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="b1e77-114">Définir les machines virtuelles par utilisateur</span><span class="sxs-lookup"><span data-stu-id="b1e77-114">Set virtual machines per user</span></span>
<span data-ttu-id="b1e77-115">La stratégie **Machines virtuelles par utilisateur** vous permet de spécifier le nombre maximal de machines virtuelles pouvant être créées par un utilisateur individuel.</span><span class="sxs-lookup"><span data-stu-id="b1e77-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="b1e77-116">Si un utilisateur tente de créer ou de revendiquer une machine virtuelle alors que le nombre limite par utilisateur est atteint, un message d’erreur indique que la machine virtuelle ne peut pas être créée/revendiquée.</span><span class="sxs-lookup"><span data-stu-id="b1e77-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="b1e77-117">Dans le menu **Configuration et stratégies** du laboratoire, sélectionnez **Machines virtuelles par utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Machines virtuelles par utilisateur](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="b1e77-119">Sélectionnez **Oui** pour limiter le nombre de machines virtuelles par utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b1e77-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="b1e77-120">Si vous ne souhaitez pas limiter le nombre de machines virtuelles par utilisateur, sélectionnez **Non**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="b1e77-121">Si vous sélectionnez **Oui**, entrez une valeur numérique indiquant le nombre maximal de machines virtuelles qu’un utilisateur peut créer ou revendiquer.</span><span class="sxs-lookup"><span data-stu-id="b1e77-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="b1e77-122">Sélectionnez **Oui** pour limiter le nombre de machines virtuelles pouvant utiliser un disque SSD.</span><span class="sxs-lookup"><span data-stu-id="b1e77-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="b1e77-123">Si vous ne souhaitez pas limiter le nombre de machines virtuelles pouvant utiliser un disque SSD, sélectionnez **Non**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="b1e77-124">Si vous sélectionnez **Oui**, entrez une valeur indiquant le nombre maximal de machines virtuelles qu’un utilisateur peut créer à l’aide d’un disque SSD.</span><span class="sxs-lookup"><span data-stu-id="b1e77-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="b1e77-125">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="b1e77-126">Définir les machines virtuelles par laboratoire</span><span class="sxs-lookup"><span data-stu-id="b1e77-126">Set virtual machines per lab</span></span>
<span data-ttu-id="b1e77-127">La stratégie **Machines virtuelles par laboratoire** vous permet de spécifier le nombre maximal de machines virtuelles pouvant être créées pour le laboratoire actuel.</span><span class="sxs-lookup"><span data-stu-id="b1e77-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="b1e77-128">Si un utilisateur tente de créer une machine virtuelle alors que le nombre limite par laboratoire est atteint, un message d’erreur indique que la machine virtuelle ne peut pas être créée.</span><span class="sxs-lookup"><span data-stu-id="b1e77-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="b1e77-129">Dans le menu **Configuration et stratégies** du laboratoire, sélectionnez **Machines virtuelles par laboratoire**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Machines virtuelles par laboratoire](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="b1e77-131">Sélectionnez **Oui** pour limiter le nombre de machines virtuelles par laboratoire.</span><span class="sxs-lookup"><span data-stu-id="b1e77-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="b1e77-132">Si vous ne souhaitez pas limiter le nombre de machines virtuelles par laboratoire, sélectionnez **Non**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="b1e77-133">Si vous sélectionnez **Oui**, entrez une valeur numérique indiquant le nombre maximal de machines virtuelles qu’un utilisateur peut créer ou revendiquer.</span><span class="sxs-lookup"><span data-stu-id="b1e77-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="b1e77-134">Sélectionnez **Oui** pour limiter le nombre de machines virtuelles pouvant utiliser un disque SSD.</span><span class="sxs-lookup"><span data-stu-id="b1e77-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="b1e77-135">Si vous ne souhaitez pas limiter le nombre de machines virtuelles pouvant utiliser un disque SSD, sélectionnez **Non**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="b1e77-136">Si vous sélectionnez **Oui**, entrez une valeur indiquant le nombre maximal de machines virtuelles qu’un utilisateur peut créer à l’aide d’un disque SSD.</span><span class="sxs-lookup"><span data-stu-id="b1e77-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="b1e77-137">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="b1e77-138">Définir l’arrêt automatique</span><span class="sxs-lookup"><span data-stu-id="b1e77-138">Set auto-shutdown</span></span>
<span data-ttu-id="b1e77-139">La stratégie d’arrêt automatique vous permet d’indiquer l’heure à laquelle les machines virtuelles du laboratoire doivent s’arrêter et contribue ainsi à réduire les pertes de laboratoire.</span><span class="sxs-lookup"><span data-stu-id="b1e77-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="b1e77-140">Dans le panneau **Configuration et stratégies**, sélectionnez **Arrêt automatique**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Arrêt automatique](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="b1e77-142">Sélectionnez **Activer** ou **Désactiver** pour activer ou désactiver cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="b1e77-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="b1e77-143">Si vous activez cette stratégie, spécifiez l’heure (et le fuseau horaire) de l’arrêt pour toutes les machines virtuelles du laboratoire actif.</span><span class="sxs-lookup"><span data-stu-id="b1e77-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="b1e77-144">Spécifiez **Oui** ou **Non** pour l’option d’envoi de notification 15 minutes avant l’heure d’arrêt automatique spécifiée.</span><span class="sxs-lookup"><span data-stu-id="b1e77-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="b1e77-145">Si vous spécifiez **Oui**, entrez un point de terminaison d’URL webhook pour recevoir la notification.</span><span class="sxs-lookup"><span data-stu-id="b1e77-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="b1e77-146">Pour plus d’informations sur les webhooks, consultez [Créer une fonction Azure d’API ou de webhook](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="b1e77-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="b1e77-147">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-147">Select **Save**.</span></span>

    <span data-ttu-id="b1e77-148">Par défaut, une fois activée, cette stratégie s’applique à toutes les machines virtuelles dans le laboratoire en cours.</span><span class="sxs-lookup"><span data-stu-id="b1e77-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="b1e77-149">Pour supprimer ce paramètre sur une machine virtuelle spécifique, ouvrez le panneau de la machine virtuelle et modifiez son paramètre **Arrêt automatique** .</span><span class="sxs-lookup"><span data-stu-id="b1e77-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="b1e77-150">Définir le démarrage automatique</span><span class="sxs-lookup"><span data-stu-id="b1e77-150">Set auto-start</span></span>
<span data-ttu-id="b1e77-151">La stratégie de démarrage automatique vous permet de spécifier quand les machines virtuelles du laboratoire doivent être démarrées.</span><span class="sxs-lookup"><span data-stu-id="b1e77-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="b1e77-152">Dans le panneau **Configuration et stratégies**, sélectionnez **Démarrage automatique**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Démarrage automatique](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="b1e77-154">Sélectionnez **Activer** ou **Désactiver** pour activer ou désactiver cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="b1e77-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="b1e77-155">Si vous activez cette stratégie, spécifiez l’heure de démarrage programmée, le fuseau horaire et les jours de la semaine auxquels cette heure s’applique.</span><span class="sxs-lookup"><span data-stu-id="b1e77-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="b1e77-156">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b1e77-156">Select **Save**.</span></span>

    <span data-ttu-id="b1e77-157">Une fois activée, cette stratégie n’est pas automatiquement appliquée à toutes les machines virtuelles dans le laboratoire en cours.</span><span class="sxs-lookup"><span data-stu-id="b1e77-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="b1e77-158">Pour appliquer ce paramètre à une machine virtuelle spécifique, ouvrez le panneau de la machine virtuelle et modifiez son paramètre **Démarrage automatique** .</span><span class="sxs-lookup"><span data-stu-id="b1e77-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="b1e77-159">Définir une date d’expiration</span><span class="sxs-lookup"><span data-stu-id="b1e77-159">Set expiration date</span></span>
<span data-ttu-id="b1e77-160">Lorsque vous [créez la machine virtuelle](devtest-lab-add-vm.md), vous pouvez définir une date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="b1e77-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="b1e77-161">Dans **Paramètres avancés**, choisissez l’icône de calendrier pour spécifier la date à laquelle la machine virtuelle doit être automatiquement supprimée.</span><span class="sxs-lookup"><span data-stu-id="b1e77-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="b1e77-162">Par défaut, la machine virtuelle n’expire jamais.</span><span class="sxs-lookup"><span data-stu-id="b1e77-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="b1e77-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1e77-163">Next steps</span></span>
<span data-ttu-id="b1e77-164">Une fois que vous avez défini et appliqué les différents paramètres de stratégies des machines virtuelles pour votre laboratoire, voici ce que vous pouvez essayer de faire :</span><span class="sxs-lookup"><span data-stu-id="b1e77-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="b1e77-165">[Comprendre les adresses IP partagées](devtest-lab-shared-ip.md) : explique comment les adresses IP partagées sont utilisées dans DevTest Labs pour réduire le nombre d’adresses IP publiques requises pour se connecter aux machines virtuelles de votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="b1e77-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="b1e77-166">[Configurer la gestion des coûts](devtest-lab-configure-cost-management.md) : montre comment utiliser le graphique **Tendance des coûts mensuels estimés**</span><span class="sxs-lookup"><span data-stu-id="b1e77-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="b1e77-167">pour afficher le coût estimé à ce jour pour le mois en cours et le coût projeté pour la fin du mois.</span><span class="sxs-lookup"><span data-stu-id="b1e77-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="b1e77-168">[Créer une image personnalisée](devtest-lab-create-template.md) : quand vous créez une machine virtuelle, vous spécifiez une base, qui peut être soit une image personnalisée, soit une image Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b1e77-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="b1e77-169">Cet article explique comment créer une image personnalisée à partir d’un fichier VHD.</span><span class="sxs-lookup"><span data-stu-id="b1e77-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="b1e77-170">[Configurer des images Marketplace](devtest-lab-configure-marketplace-images.md) : Azure DevTest Labs prend en charge la création de machines virtuelles basées sur des images Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b1e77-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="b1e77-171">Cet article explique comment spécifier, le cas échéant, les images Azure Marketplace pouvant être utilisées lors de la création de machines virtuelles dans un laboratoire.</span><span class="sxs-lookup"><span data-stu-id="b1e77-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="b1e77-172">[Créer une machine virtuelle dans un laboratoire](devtest-lab-add-vm-with-artifacts.md) : montre comment créer une machine virtuelle à partir d’une image de base (personnalisée ou Marketplace) et comment utiliser des artefacts dans votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b1e77-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

