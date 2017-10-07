---
title: "aaaCreate un réseau virtuel Azure d’homologation - Gestionnaire de ressources - même abonnement | Documents Microsoft"
description: "Découvrez comment toocreate une homologation de réseau virtuel entre des réseaux virtuels créés via le Gestionnaire de ressources qui existent dans hello même abonnement Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="51215-103">Créer une homologation de réseaux virtuels - Resource Manager - Même abonnement</span><span class="sxs-lookup"><span data-stu-id="51215-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="51215-104">Dans ce didacticiel, vous découvrez toocreate un réseau virtuel d’homologation entre réseaux virtuels créés par le biais du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="51215-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="51215-105">Les deux réseaux virtuels existe dans hello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="51215-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="51215-106">D’homologation deux réseaux virtuels Active ressources toocommunicate différents réseaux virtuels entre eux avec hello même la bande passante et la latence comme si les ressources hello étaient hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="51215-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="51215-107">En savoir plus sur l’[homologation de réseaux virtuels](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51215-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="51215-108">Hello étapes toocreate une homologation de réseau virtuel sont différents, selon que les réseaux virtuels hello sont dans hello identiques ou différent, les abonnements et qui [modèle de déploiement Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello des réseaux virtuels sont créés via.</span><span class="sxs-lookup"><span data-stu-id="51215-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="51215-109">Découvrez comment toocreate a virtual network homologation dans d’autres scénarios en cliquant sur le scénario hello hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="51215-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="51215-110">Modèle de déploiement Azure</span><span class="sxs-lookup"><span data-stu-id="51215-110">Azure deployment model</span></span>  | <span data-ttu-id="51215-111">Abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="51215-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="51215-112">Deux modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="51215-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="51215-113">Différent</span><span class="sxs-lookup"><span data-stu-id="51215-113">Different</span></span>|
|[<span data-ttu-id="51215-114">Un modèle Resource Manager, un modèle classique</span><span class="sxs-lookup"><span data-stu-id="51215-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="51215-115">Identique</span><span class="sxs-lookup"><span data-stu-id="51215-115">Same</span></span>|
|[<span data-ttu-id="51215-116">Un modèle Resource Manager, un modèle classique</span><span class="sxs-lookup"><span data-stu-id="51215-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="51215-117">Différent</span><span class="sxs-lookup"><span data-stu-id="51215-117">Different</span></span>|

<span data-ttu-id="51215-118">Une homologation de réseau virtuel ne peut pas être créée entre deux réseaux virtuels déployés via le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="51215-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="51215-119">Une homologation de réseau virtuel ne peut être créée qu’entre deux réseaux virtuels qui existent dans hello même région Azure.</span><span class="sxs-lookup"><span data-stu-id="51215-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="51215-120">Si vous devez tooconnect des réseaux virtuels qui ont été créés via le modèle de déploiement classique de hello, ou qui existe dans différentes régions Azure, vous pouvez utiliser Azure [passerelle VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="51215-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="51215-121">Vous pouvez utiliser hello [portail Azure](#portal), hello Azure [une interface de ligne](#cli) (CLI), Azure [PowerShell](#powershell), ou une [le modèle Azure Resource Manager](#template) toocreate une homologation de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="51215-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="51215-122">Cliquez sur un des hello précédente outil liens toogo directement toohello les étapes de création d’une homologation de réseau virtuel à l’aide de votre outil de choix.</span><span class="sxs-lookup"><span data-stu-id="51215-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="51215-123"><a name="portal"></a>Créer une homologation - portail Azure</span><span class="sxs-lookup"><span data-stu-id="51215-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="51215-124">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="51215-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="51215-125">compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="51215-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="51215-126">Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="51215-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="51215-127">Cliquez sur **+ Nouveau**, puis sur **Mise en réseau** et **Réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="51215-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="51215-128">Bonjour **créer un réseau virtuel** panneau, puis entrez ou sélectionnez les valeurs pour hello suivant les paramètres, **créer**:</span><span class="sxs-lookup"><span data-stu-id="51215-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="51215-129">**Nom** : *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="51215-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="51215-130">**Espace d’adressage** : *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="51215-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="51215-131">**Nom du sous-réseau** : *par défaut*</span><span class="sxs-lookup"><span data-stu-id="51215-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="51215-132">**Espace d’adressage de sous-réseau** : *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="51215-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="51215-133">**Abonnement** : sélectionnez votre abonnement</span><span class="sxs-lookup"><span data-stu-id="51215-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="51215-134">**Groupe de ressources** : sélectionnez **Créer** et entrez *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="51215-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="51215-135">**Emplacement** : *États-Unis de l’Est*</span><span class="sxs-lookup"><span data-stu-id="51215-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="51215-136">Effectuez les étapes 2 et 3 à nouveau en spécifiant hello suivant à l’étape 3 :</span><span class="sxs-lookup"><span data-stu-id="51215-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="51215-137">**Nom** : *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="51215-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="51215-138">**Espace d’adressage** : *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="51215-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="51215-139">**Nom du sous-réseau** : *par défaut*</span><span class="sxs-lookup"><span data-stu-id="51215-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="51215-140">**Espace d’adressage de sous-réseau** : *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="51215-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="51215-141">**Abonnement** : sélectionnez votre abonnement</span><span class="sxs-lookup"><span data-stu-id="51215-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="51215-142">**Groupe de ressources** : sélectionnez **Use existing** (Utiliser existant), puis *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="51215-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="51215-143">**Emplacement** : *États-Unis de l’Est*</span><span class="sxs-lookup"><span data-stu-id="51215-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="51215-144">Bonjour **recherche les ressources** zone en haut hello hello du portail de, type *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="51215-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="51215-145">Cliquez sur **myResourceGroup** lorsqu’il apparaît dans les résultats de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="51215-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="51215-146">Un panneau s’affiche pour hello **myresourcegroup** groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="51215-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="51215-147">groupe de ressources Hello contient hello deux réseaux virtuels créés dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="51215-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="51215-148">Cliquez sur **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="51215-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="51215-149">Bonjour **myVnet1** panneau qui s’affiche, cliquez sur **homologations** de liste verticale de hello des options sur hello gauche du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="51215-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="51215-150">Bonjour **myVnet1 - homologations** panneau s’affiche, cliquez sur **+ ajouter**</span><span class="sxs-lookup"><span data-stu-id="51215-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="51215-151">Bonjour **ajouter d’homologation** panneau qui s’affiche, entrez, ou sélectionnez hello options suivantes, puis cliquez sur **OK**:</span><span class="sxs-lookup"><span data-stu-id="51215-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="51215-152">**Nom** : *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="51215-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="51215-153">**Modèle de déploiement de réseau virtuel** : sélectionnez **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="51215-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="51215-154">**Abonnement** : sélectionnez votre abonnement</span><span class="sxs-lookup"><span data-stu-id="51215-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="51215-155">**Réseau virtuel** : cliquez sur **Choisir un réseau virtuel**, puis sur **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="51215-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="51215-156">**Autoriser l’accès au réseau virtuel :** vérifiez que l’option **Activé** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="51215-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="51215-157">Il n’y aucun autre paramètre utilisé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="51215-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="51215-158">toolearn sur tous les paramètres d’homologation, lire [gérer homologations de réseaux virtuels](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="51215-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="51215-159">Après avoir cliqué sur **OK** à l’étape précédente de hello, hello **ajouter d’homologation** panneau se ferme et vous voyez hello **myVnet1 - homologations** panneau à nouveau.</span><span class="sxs-lookup"><span data-stu-id="51215-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="51215-160">Après quelques secondes, hello d’homologation que vous avez créé s’affiche dans le panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="51215-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="51215-161">**Initiée par** est répertorié dans hello **d’homologation de statut** colonne hello **myVnet1ToMyVnet2** d’homologation vous créé.</span><span class="sxs-lookup"><span data-stu-id="51215-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="51215-162">Vous avez homologuer tooVnet2 de Vnet1, mais vous devez maintenant homologue myVnet2 toomyVnet1.</span><span class="sxs-lookup"><span data-stu-id="51215-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="51215-163">Hello d’homologation doit être créé dans les deux sens tooenable ressources toocommunicate de réseaux virtuels hello entre eux.</span><span class="sxs-lookup"><span data-stu-id="51215-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="51215-164">Répétez les étapes 5 à 10 pour myVnet2.</span><span class="sxs-lookup"><span data-stu-id="51215-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="51215-165">Homologation de nom hello *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="51215-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="51215-166">Quelques secondes après avoir cliqué sur **OK** toocreate hello d’homologation pour MyVnet2, hello **myVnet2ToMyVnet1** d’homologation vous venez de créer est répertorié avec **connecté** Bonjour  **ÉTAT de l’homologation** colonne.</span><span class="sxs-lookup"><span data-stu-id="51215-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="51215-167">Répétez les étapes 5 à 7 pour MyVnet1.</span><span class="sxs-lookup"><span data-stu-id="51215-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="51215-168">Hello **d’homologation de statut** pour hello **myVnet1ToVNet2** d’homologation est désormais également **connecté**.</span><span class="sxs-lookup"><span data-stu-id="51215-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="51215-169">Hello d’homologation est établie avec succès une fois que vous **connecté** Bonjour **d’homologation de statut** colonne pour les deux réseaux virtuels dans l’homologation de hello.</span><span class="sxs-lookup"><span data-stu-id="51215-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="51215-170">**Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.</span><span class="sxs-lookup"><span data-stu-id="51215-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="51215-171">**Facultatif**: toodelete ressources hello que vous créez dans ce didacticiel, les étapes hello complète Bonjour [supprimer des ressources](#delete-portal) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="51215-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="51215-172">Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="51215-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="51215-173">Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="51215-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="51215-174">Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="51215-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="51215-175">Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="51215-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="51215-176"><a name="cli"></a>Créer une homologation - interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="51215-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="51215-177">Hello le script suivant :</span><span class="sxs-lookup"><span data-stu-id="51215-177">hello following script:</span></span>

- <span data-ttu-id="51215-178">Requiert hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="51215-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="51215-179">version de hello toofind, exécutez hello `az --version` commande.</span><span class="sxs-lookup"><span data-stu-id="51215-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="51215-180">Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51215-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="51215-181">Fonctionne dans un interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="51215-181">Works in a Bash shell.</span></span> <span data-ttu-id="51215-182">Pour les options sur l’exécution de scripts CLI d’Azure sur le client Windows, consultez [hello CLI d’Azure en cours d’exécution dans Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51215-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="51215-183">Au lieu d’installer hello CLI et ses dépendances, vous pouvez utiliser hello Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="51215-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="51215-184">Bonjour Azure Cloud Shell est un interpréteur de commandes Bash gratuit que vous pouvez exécuter directement à l’intérieur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="51215-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="51215-185">Il a hello CLI d’Azure préinstallé et configuré toouse avec votre compte.</span><span class="sxs-lookup"><span data-stu-id="51215-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="51215-186">Cliquez sur hello **essayez-la** bouton dans le script hello qui suit, ce qui permet d’appeler un environnement de Cloud qui vous connecte peut se connecter tooyour compte Azure avec.</span><span class="sxs-lookup"><span data-stu-id="51215-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="51215-187">tooexecute hello script, cliquez sur hello **copie** bouton et coller le contenu hello dans votre environnement Cloud.</span><span class="sxs-lookup"><span data-stu-id="51215-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="51215-188">Créez un groupe de ressources et deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="51215-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="51215-189">Créez un réseau virtuel d’homologation entre les réseaux virtuels deux hello.</span><span class="sxs-lookup"><span data-stu-id="51215-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="51215-190">Après l’exécution du script de hello, passez en revue les homologations hello pour chaque réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="51215-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="51215-191">Exécuter la commande précédente hello à nouveau, en remplaçant *myVnet1* avec *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="51215-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="51215-192">sortie Hello des deux commandes montre **connecté** Bonjour **PeeringState** colonne.</span><span class="sxs-lookup"><span data-stu-id="51215-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="51215-193">Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="51215-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="51215-194">Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="51215-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="51215-195">Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="51215-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="51215-196">Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="51215-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="51215-197">**Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.</span><span class="sxs-lookup"><span data-stu-id="51215-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="51215-198">**Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-cli) dans cet article.</span><span class="sxs-lookup"><span data-stu-id="51215-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="51215-199"><a name="powershell"></a>Créer une homologation - PowerShell</span><span class="sxs-lookup"><span data-stu-id="51215-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="51215-200">Installer la version la plus récente de hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span><span class="sxs-lookup"><span data-stu-id="51215-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="51215-201">Si vous êtes nouveau tooAzure PowerShell, consultez [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51215-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="51215-202">toostart une session de PowerShell, consultez trop**Démarrer**, entrez **powershell**, puis cliquez sur **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="51215-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="51215-203">Dans PowerShell, connectez-vous tooAzure en entrant hello `login-azurermaccount` commande.</span><span class="sxs-lookup"><span data-stu-id="51215-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="51215-204">compte de Hello avec que vous vous connectez doit avoir toocreate des autorisations nécessaires hello une homologation de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="51215-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="51215-205">Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="51215-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="51215-206">Créez un groupe de ressources et deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="51215-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="51215-207">script de hello tooexecute, copie hello suivantes de script, collez-le dans PowerShell et appuyez sur `Enter` après la dernière ligne de hello s’affiche sur l’écran hello :</span><span class="sxs-lookup"><span data-stu-id="51215-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="51215-208">Créez un réseau virtuel d’homologation entre les réseaux virtuels deux hello.</span><span class="sxs-lookup"><span data-stu-id="51215-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="51215-209">Copie hello suivantes de script, collez dans tooPowerShell et appuyez sur `Enter` après la dernière ligne de hello s’affiche sur l’écran hello :</span><span class="sxs-lookup"><span data-stu-id="51215-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="51215-210">tooreview des sous-réseaux hello pour le réseau virtuel de hello, copie hello suivantes de commande, collez dans tooPowerShell et appuyez sur `Enter`:</span><span class="sxs-lookup"><span data-stu-id="51215-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="51215-211">Exécuter la commande précédente hello à nouveau, en remplaçant *myVnet1* avec *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="51215-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="51215-212">sortie Hello des deux commandes montre **connecté** Bonjour **PeeringState** colonne.</span><span class="sxs-lookup"><span data-stu-id="51215-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="51215-213">**Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.</span><span class="sxs-lookup"><span data-stu-id="51215-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="51215-214">**Facultatif**: hello complète toodelete ressources hello que vous créez dans ce didacticiel, les étapes [supprimer des ressources](#delete-powershell) dans cet article.</span><span class="sxs-lookup"><span data-stu-id="51215-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="51215-215">Les ressources Azure que vous créez dans un réseau virtuel sont désormais en mesure de toocommunicate entre eux via leurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="51215-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="51215-216">Si vous utilisez la résolution de noms Azure par défaut pour les réseaux virtuels hello, hello ressources dans des réseaux virtuels hello ne sont pas en mesure de tooresolve noms sur des réseaux virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="51215-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="51215-217">Si vous voulez que les noms de tooresolve sur plusieurs réseaux virtuels dans une homologation, vous devez créer votre propre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="51215-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="51215-218">Découvrez comment tooset des [à l’aide de votre propre serveur DNS de résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="51215-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="51215-219"><a name="template"></a>Créer une homologation - modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="51215-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="51215-220">Faites référence au modèle Azure Resource Manager [Créer une homologation de réseaux virtuels](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering).</span><span class="sxs-lookup"><span data-stu-id="51215-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="51215-221">Les instructions sont fournies avec le modèle hello pour le déploiement de modèle de hello à l’aide de hello portail Azure, PowerShell ou hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="51215-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="51215-222">Journal dans l’outil toowhichever vous choisissez modèle hello toodeploy à l’aide d’un compte qui dispose hello toocreate des autorisations nécessaires à un réseau virtuel d’homologation.</span><span class="sxs-lookup"><span data-stu-id="51215-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="51215-223">Consultez hello [autorisations](#permissions) section de cet article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="51215-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="51215-224">**Facultatif**: bien que la création d’ordinateurs virtuels n’est pas abordé dans ce didacticiel, vous pouvez créer une machine virtuelle de chaque réseau virtuel et vous connecter à partir d’un ordinateur virtuel toohello autres toovalidate connectivité.</span><span class="sxs-lookup"><span data-stu-id="51215-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="51215-225">**Facultatif**: toodelete ressources hello que vous créez dans ce didacticiel, les étapes hello complète Bonjour [supprimer des ressources](#delete) section de cet article, à l’aide hello portail Azure, PowerShell ou hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="51215-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="51215-226"><a name="permissions"></a>Autorisations</span><span class="sxs-lookup"><span data-stu-id="51215-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="51215-227">Hello tous les comptes toocreate une homologation de réseau virtuel doivent avoir hello nécessaires ou autorisations.</span><span class="sxs-lookup"><span data-stu-id="51215-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="51215-228">Par exemple, si vous ont été homologation deux réseaux virtuels nommés VNet1 et VNet2, doit être affecté à votre compte hello suivant rôle minimale ou les autorisations pour chaque réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="51215-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="51215-229">Réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="51215-229">Virtual network</span></span>|<span data-ttu-id="51215-230">Rôle</span><span class="sxs-lookup"><span data-stu-id="51215-230">Role</span></span>|<span data-ttu-id="51215-231">Autorisations</span><span class="sxs-lookup"><span data-stu-id="51215-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="51215-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="51215-232">VNet1</span></span>|[<span data-ttu-id="51215-233">Collaborateur de réseau</span><span class="sxs-lookup"><span data-stu-id="51215-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="51215-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="51215-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="51215-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="51215-235">VNet2</span></span>|[<span data-ttu-id="51215-236">Collaborateur de réseau</span><span class="sxs-lookup"><span data-stu-id="51215-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="51215-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="51215-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="51215-238">En savoir plus sur [rôles intégrés](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) et l’affectation des autorisations spécifiques trop[des rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager uniquement).</span><span class="sxs-lookup"><span data-stu-id="51215-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="51215-239"><a name="delete"></a>Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="51215-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="51215-240">Lorsque vous avez terminé ce didacticiel, vous pourriez les ressources de hello toodelete que vous avez créé dans le didacticiel de hello, donc vous ne subissez des frais d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="51215-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="51215-241">Suppression d’un groupe de ressources supprime également toutes les ressources qui se trouvent dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="51215-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="51215-242"><a name="delete-portal"></a>Portail Azure</span><span class="sxs-lookup"><span data-stu-id="51215-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="51215-243">Dans la zone de recherche du portail hello, entrez **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="51215-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="51215-244">Dans les résultats de recherche de hello, cliquez sur **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="51215-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="51215-245">Sur hello **myResourceGroup** panneau, cliquez sur hello **supprimer** icône.</span><span class="sxs-lookup"><span data-stu-id="51215-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="51215-246">suppression de hello tooconfirm, Bonjour **hello TYPE nom groupe de ressources** , entrez **myResourceGroup**, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="51215-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="51215-247"><a name="delete-cli"></a>Interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="51215-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="51215-248">Entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="51215-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="51215-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="51215-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="51215-250">Entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="51215-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="51215-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51215-251">Next steps</span></span>

- <span data-ttu-id="51215-252">Familiarisez-vous bien avec les [comportements et contraintes importants de l’homologation de réseaux virtuels](virtual-network-manage-peering.md#requirements-and-constraints) avant d’en créer une pour une utilisation en production.</span><span class="sxs-lookup"><span data-stu-id="51215-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="51215-253">Apprenez-en davantage sur tous les [paramètres d’homologation de réseaux virtuels](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="51215-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="51215-254">Découvrez comment trop[créer un hub et spoke topologie de réseau](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) avec le réseau virtuel d’homologation.</span><span class="sxs-lookup"><span data-stu-id="51215-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
