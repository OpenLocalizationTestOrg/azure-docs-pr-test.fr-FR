---
title: "stratégies de laboratoire aaaManage dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment les stratégies de laboratoire toodefine tels que des ordinateurs virtuels tailles, nombre maximal de machines virtuelles par utilisateur et l’automatisation de l’arrêt."
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
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="57eba-103">Gérer toutes les stratégies d’un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="57eba-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="57eba-104">Azure DevTest Labs vous permet de contrôler les coûts et de réduire le gaspillage dans vos laboratoires en gérant les stratégies (paramètres) de chacun d’entre eux.</span><span class="sxs-lookup"><span data-stu-id="57eba-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="57eba-105">Cet article explique étape par étape en détail comment tooset chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="57eba-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="57eba-106">Définir les tailles de machine virtuelle autorisées</span><span class="sxs-lookup"><span data-stu-id="57eba-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="57eba-107">Hello stratégie pour hello de paramètre autorisés tailles de machine virtuelle permet toominimize lab déchets en vous toospecify les tailles des machines virtuelles sont autorisées dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="57eba-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="57eba-108">Si cette stratégie est activée, uniquement les tailles de machine virtuelle à partir de cette liste peuvent être utilisé toocreate VMs.</span><span class="sxs-lookup"><span data-stu-id="57eba-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="57eba-109">Sur du laboratoire hello **stratégies de Configuration et** panneau, sélectionnez **tailles de machines virtuelles autorisées**.</span><span class="sxs-lookup"><span data-stu-id="57eba-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Tailles de machine virtuelle autorisées](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="57eba-111">Sélectionnez **sur** tooenable cette stratégie, et **hors** toodisable il.</span><span class="sxs-lookup"><span data-stu-id="57eba-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="57eba-112">Si vous activez cette stratégie, sélectionnez une ou plusieurs tailles de machine virtuelle pouvant être créées dans votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="57eba-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="57eba-113">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="57eba-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="57eba-114">Définir les machines virtuelles par utilisateur</span><span class="sxs-lookup"><span data-stu-id="57eba-114">Set virtual machines per user</span></span>
<span data-ttu-id="57eba-115">Hello stratégie pour **machines virtuelles par utilisateur** vous permet de toospecify hello nombre de machines virtuelles qui peuvent être créés par un utilisateur individuel.</span><span class="sxs-lookup"><span data-stu-id="57eba-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="57eba-116">Si un utilisateur tente de toocreate ou la revendication d’une machine virtuelle lors de la limite d’utilisateurs hello a été atteint, un message d’erreur indique que hello que machine virtuelle ne peut pas être créé/demandé.</span><span class="sxs-lookup"><span data-stu-id="57eba-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="57eba-117">Sur du laboratoire hello **stratégies de Configuration et** menu, sélectionnez **machines virtuelles par utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="57eba-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Machines virtuelles par utilisateur](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="57eba-119">Sélectionnez **Oui** toolimit hello plusieurs ordinateurs virtuels par utilisateur.</span><span class="sxs-lookup"><span data-stu-id="57eba-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="57eba-120">Si vous ne souhaitez pas toolimit hello plusieurs ordinateurs virtuels par utilisateur, sélectionnez **non**.</span><span class="sxs-lookup"><span data-stu-id="57eba-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="57eba-121">Si vous sélectionnez **Oui**, entrez une valeur numérique indiquant le nombre maximal de hello de machines virtuelles qui peuvent être créés ou demandé par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="57eba-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="57eba-122">Sélectionnez **Oui** nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD (SSD).</span><span class="sxs-lookup"><span data-stu-id="57eba-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="57eba-123">Si vous ne souhaitez pas le nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD, sélectionnez **non**.</span><span class="sxs-lookup"><span data-stu-id="57eba-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="57eba-124">Si vous sélectionnez **Oui**, entrez une valeur qui indique le nombre maximal de hello de machines virtuelles qui peuvent être créés à l’aide de disques SSD.</span><span class="sxs-lookup"><span data-stu-id="57eba-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="57eba-125">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="57eba-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="57eba-126">Définir les machines virtuelles par laboratoire</span><span class="sxs-lookup"><span data-stu-id="57eba-126">Set virtual machines per lab</span></span>
<span data-ttu-id="57eba-127">Hello stratégie pour **machines virtuelles par lab** vous permet de toospecify hello nombre de machines virtuelles qui peuvent être créés pour les pratiques hello.</span><span class="sxs-lookup"><span data-stu-id="57eba-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="57eba-128">Si un utilisateur tente toocreate une machine virtuelle lors de la limite de laboratoire hello a été atteint, un message d’erreur indique que hello que machine virtuelle ne peut pas être créé.</span><span class="sxs-lookup"><span data-stu-id="57eba-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="57eba-129">Sur du laboratoire hello **stratégies de Configuration et** menu, sélectionnez **machines virtuelles par lab**.</span><span class="sxs-lookup"><span data-stu-id="57eba-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Machines virtuelles par laboratoire](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="57eba-131">Sélectionnez **Oui** toolimit hello différentes machines virtuelles par lab.</span><span class="sxs-lookup"><span data-stu-id="57eba-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="57eba-132">Si vous ne souhaitez pas le nombre de hello toolimit de machines virtuelles par lab, sélectionnez **non**.</span><span class="sxs-lookup"><span data-stu-id="57eba-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="57eba-133">Si vous sélectionnez **Oui**, entrez une valeur numérique indiquant le nombre maximal de hello de machines virtuelles qui peuvent être créés ou demandé par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="57eba-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="57eba-134">Sélectionnez **Oui** nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD (SSD).</span><span class="sxs-lookup"><span data-stu-id="57eba-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="57eba-135">Si vous ne souhaitez pas le nombre de hello toolimit de machines virtuelles que vous pouvez utiliser des disques SSD, sélectionnez **non**.</span><span class="sxs-lookup"><span data-stu-id="57eba-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="57eba-136">Si vous sélectionnez **Oui**, entrez une valeur qui indique le nombre maximal de hello de machines virtuelles qui peuvent être créés à l’aide de disques SSD.</span><span class="sxs-lookup"><span data-stu-id="57eba-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="57eba-137">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="57eba-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="57eba-138">Définir l’arrêt automatique</span><span class="sxs-lookup"><span data-stu-id="57eba-138">Set auto-shutdown</span></span>
<span data-ttu-id="57eba-139">stratégie d’arrêt automatique Hello permet toominimize lab déchets, ce qui permet des temps de hello toospecify permettant d’arrêter des machines virtuelles de ce laboratoire.</span><span class="sxs-lookup"><span data-stu-id="57eba-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="57eba-140">Sur du laboratoire hello **stratégies de Configuration et** panneau, sélectionnez **arrêt automatique**.</span><span class="sxs-lookup"><span data-stu-id="57eba-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Arrêt automatique](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="57eba-142">Sélectionnez **sur** tooenable cette stratégie, et **hors** toodisable il.</span><span class="sxs-lookup"><span data-stu-id="57eba-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="57eba-143">Si vous activez cette stratégie, spécifiez tooshut de temps (et le fuseau horaire) hello tous les ordinateurs virtuels vers le bas dans le lab actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="57eba-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="57eba-144">Spécifiez **Oui** ou **non** pour hello option toosend un toohello préalable de 15 minutes de notification spécifié des temps d’arrêt automatique.</span><span class="sxs-lookup"><span data-stu-id="57eba-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="57eba-145">Si vous spécifiez **Oui**, entrez une notification de webhook URL du point de terminaison tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="57eba-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="57eba-146">Pour plus d’informations sur les webhooks, consultez [Créer une fonction Azure d’API ou de webhook](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="57eba-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="57eba-147">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="57eba-147">Select **Save**.</span></span>

    <span data-ttu-id="57eba-148">Par défaut, une fois activée, cette stratégie s’applique des machines virtuelles tooall pratiques hello.</span><span class="sxs-lookup"><span data-stu-id="57eba-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="57eba-149">tooremove ce paramètre à partir d’un ordinateur virtuel spécifique, ouvrir le panneau et la modification de la machine virtuelle hello son **arrêt automatique** paramètre</span><span class="sxs-lookup"><span data-stu-id="57eba-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="57eba-150">Définir le démarrage automatique</span><span class="sxs-lookup"><span data-stu-id="57eba-150">Set auto-start</span></span>
<span data-ttu-id="57eba-151">permet de stratégie de démarrage automatique Hello vous toospecify hello machines virtuelles dans le lab actuel de hello doit être démarré.</span><span class="sxs-lookup"><span data-stu-id="57eba-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="57eba-152">Sur du laboratoire hello **stratégies de Configuration et** panneau, sélectionnez **démarrage automatique**.</span><span class="sxs-lookup"><span data-stu-id="57eba-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Démarrage automatique](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="57eba-154">Sélectionnez **sur** tooenable cette stratégie, et **hors** toodisable il.</span><span class="sxs-lookup"><span data-stu-id="57eba-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="57eba-155">Si vous activez cette stratégie, spécifiez l’heure de début planifiée de hello, fuseau horaire et hello les jours de semaine hello pour le hello temps s’applique.</span><span class="sxs-lookup"><span data-stu-id="57eba-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="57eba-156">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="57eba-156">Select **Save**.</span></span>

    <span data-ttu-id="57eba-157">Une fois activée, cette stratégie n’est pas appliqué automatiquement tooany VM dans pratiques hello.</span><span class="sxs-lookup"><span data-stu-id="57eba-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="57eba-158">tooapply tooa de ce paramètre ordinateur virtuel spécifique, la machine virtuelle hello ouvrir Panneau et change son **démarrage automatique** paramètre</span><span class="sxs-lookup"><span data-stu-id="57eba-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="57eba-159">Définir une date d’expiration</span><span class="sxs-lookup"><span data-stu-id="57eba-159">Set expiration date</span></span>
<span data-ttu-id="57eba-160">Vous pouvez définir un délai d’expiration date à laquelle vous [créer hello VM](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="57eba-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="57eba-161">Dans **paramètres avancés**, choisissez toospecify d’icône de calendrier hello une date sur laquelle hello machine virtuelle est automatiquement supprimée.</span><span class="sxs-lookup"><span data-stu-id="57eba-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="57eba-162">Par défaut, hello VM n’expirera jamais.</span><span class="sxs-lookup"><span data-stu-id="57eba-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="57eba-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57eba-163">Next steps</span></span>
<span data-ttu-id="57eba-164">Une fois que vous avez définies et appliquées hello différents paramètres de stratégie de machine virtuelle pour votre laboratoire, Voici certaines choses tootry suivant :</span><span class="sxs-lookup"><span data-stu-id="57eba-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="57eba-165">[Comprendre les adresses IP partagées](devtest-lab-shared-ip.md) -explique comment partagé IP adresses sont utilisées dans le nombre de hello DevTest Labs toominimize du laboratoire tooyour publique IP adresses requis tooconnect machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="57eba-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="57eba-166">[Configurer la gestion des coûts](devtest-lab-configure-cost-management.md) -illustre comment toouse hello **tendance du coût estimé mensuel** graphique</span><span class="sxs-lookup"><span data-stu-id="57eba-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="57eba-167">tooview hello estimé coût-to-date du mois en cours et coût de fin de mois de hello projeté.</span><span class="sxs-lookup"><span data-stu-id="57eba-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="57eba-168">[Créer une image personnalisée](devtest-lab-create-template.md) : quand vous créez une machine virtuelle, vous spécifiez une base, qui peut être soit une image personnalisée, soit une image Marketplace.</span><span class="sxs-lookup"><span data-stu-id="57eba-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="57eba-169">Cet article explique comment toocreate personnalisé de l’image à partir d’un fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="57eba-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="57eba-170">[Configurer des images Marketplace](devtest-lab-configure-marketplace-images.md) : Azure DevTest Labs prend en charge la création de machines virtuelles basées sur des images Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="57eba-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="57eba-171">Cet article explique comment toospecify qui, le cas échéant, les images Azure Marketplace peuvent être utilisés lors de la création de machines virtuelles dans un laboratoire.</span><span class="sxs-lookup"><span data-stu-id="57eba-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="57eba-172">[Créer une machine virtuelle dans un laboratoire](devtest-lab-add-vm-with-artifacts.md) -illustre comment toocreate une machine virtuelle à partir d’une image de base (soit personnalisé ou Marketplace) et comment toowork des artefacts dans votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57eba-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

