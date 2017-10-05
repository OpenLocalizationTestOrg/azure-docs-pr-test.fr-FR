---
title: "Gérer les groupes de sécurité réseau à partir du portail Azure | Microsoft Docs"
description: "Apprenez à gérer les groupes de sécurité réseau existants à partir du portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: e9bcf8a893ff209337f6a5763b631a22f8514e20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-nsgs-using-the-portal"></a><span data-ttu-id="f36e7-103">Gérer les groupes de sécurité réseau à partir du portail</span><span class="sxs-lookup"><span data-stu-id="f36e7-103">Manage NSGs using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f36e7-104">Portail</span><span class="sxs-lookup"><span data-stu-id="f36e7-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="f36e7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f36e7-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="f36e7-106">interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f36e7-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f36e7-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f36e7-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f36e7-108">Cet article traite de l’utilisation du modèle de déploiement Resource Manager que Microsoft recommande pour la plupart des nouveaux déploiements à la place du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="f36e7-108">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="f36e7-109">Récupérer des informations</span><span class="sxs-lookup"><span data-stu-id="f36e7-109">Retrieve Information</span></span>
<span data-ttu-id="f36e7-110">Vous pouvez afficher vos groupes de sécurité réseau existants, récupérer des règles pour un groupe de sécurité réseau existant et découvrir quelles sont les ressources associées à un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f36e7-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="f36e7-111">Afficher les groupes de sécurité réseau existants</span><span class="sxs-lookup"><span data-stu-id="f36e7-111">View existing NSGs</span></span>

<span data-ttu-id="f36e7-112">Pour afficher tous les groupes de sécurité réseau existants d’un abonnement, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-112">To view all existing NSGs in a subscription, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-113">Dans un navigateur, accédez à http://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f36e7-113">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="f36e7-114">Cliquez sur **Parcourir >** > **Groupes de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="f36e7-116">Consultez la liste des groupes de sécurité réseau dans le panneau **Groupes de sécurité réseau** .</span><span class="sxs-lookup"><span data-stu-id="f36e7-116">Check the list of NSGs in the **Network security groups** blade.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="f36e7-118">Afficher les groupes de sécurité réseau d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f36e7-118">View NSGs in a resource group</span></span>

<span data-ttu-id="f36e7-119">Pour afficher la liste des groupes de sécurité réseau dans le groupe de ressources **RG-NSG**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-119">To view the list of NSGs in the **RG-NSG** resource group, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-120">Cliquez sur **Groupes de ressources >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="f36e7-122">Dans la liste des ressources, recherchez des éléments qui affichent l’icône du groupe de sécurité réseau, comme indiqué dans le panneau **Ressources** ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f36e7-122">In the list of resources, look for items displaying the NSG icon, as shown in the **Resources** blade below.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="f36e7-124">Répertorier toutes les règles pour un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="f36e7-124">List all rules for an NSG</span></span>

<span data-ttu-id="f36e7-125">Pour afficher les règles d’un groupe de sécurité réseau nommé **NSG-FrontEnd**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-125">To view the rules of an NSG named **NSG-FrontEnd**, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-126">Dans le panneau **Groupes de sécurité réseau** ou le panneau **Ressources** présenté ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-126">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="f36e7-127">Sous l’onglet **Paramètres**, cliquez sur **Règles de sécurité de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-127">In the **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="f36e7-129">Le panneau **Règles de sécurité de trafic entrant** s’affiche comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f36e7-129">The **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="f36e7-131">Sous l’onglet **Paramètres**, cliquez sur **Règles de sécurité de trafic sortant** pour afficher les règles de trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="f36e7-131">In the **Settings** tab, click **Outbound security rules** to see the outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f36e7-132">Pour afficher les règles par défaut, cliquez sur l’icône **Règles par défaut** en haut du panneau qui affiche les règles.</span><span class="sxs-lookup"><span data-stu-id="f36e7-132">To view default rules, click the **Default rules** icon at the top of the blade that displays the rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="f36e7-133">Afficher les associations de groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="f36e7-133">View NSGs associations</span></span>

<span data-ttu-id="f36e7-134">Pour afficher les ressources auxquelles le groupe de sécurité réseau **NSG-FrontEnd** est associé, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-134">To view what resources the **NSG-FrontEnd** NSG is associate with, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-135">Dans le panneau **Groupes de sécurité réseau** ou le panneau **Ressources** présenté ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-135">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="f36e7-136">Sous l’onglet **Paramètres**, cliquez sur **Sous-réseaux** pour afficher les sous-réseaux associés au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f36e7-136">In the **Settings** tab, click **Subnets** to view what subnets are associated to the NSG.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="f36e7-138">Sous l’onglet **Paramètres**, cliquez sur **Interfaces réseau** pour afficher les cartes réseau associées au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f36e7-138">In the **Settings** tab, click **Network interfaces** to view what NICs are associated to the NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="f36e7-139">Gérer les règles</span><span class="sxs-lookup"><span data-stu-id="f36e7-139">Manage rules</span></span>
<span data-ttu-id="f36e7-140">Vous pouvez ajouter des règles à un groupe de sécurité réseau existant, modifier des règles existantes et supprimer des règles.</span><span class="sxs-lookup"><span data-stu-id="f36e7-140">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="f36e7-141">Ajouter une règle</span><span class="sxs-lookup"><span data-stu-id="f36e7-141">Add a rule</span></span>
<span data-ttu-id="f36e7-142">Pour ajouter une règle autorisant le trafic **entrant** sur le port **443** d’une machine vers le groupe de sécurité réseau **NSG-FrontEnd**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-142">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-143">Dans le panneau **Groupes de sécurité réseau** ou le panneau **Ressources** présenté ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-143">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="f36e7-144">Sous l’onglet **Paramètres**, cliquez sur **Règles de sécurité de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-144">In the **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="f36e7-145">Dans le panneau **Règles de sécurité de trafic entrant**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-145">In the **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="f36e7-146">Ensuite, dans le panneau **Ajouter une règle de sécurité de trafic entrant**, fournissez les valeurs indiquées ci-dessous, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-146">Then, in the **Add inbound security rule** blade, fill the values as shown below, and then click **OK**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="f36e7-148">Après quelques secondes, notez la nouvelle règle dans le panneau **Règles de sécurité de trafic entrant** .</span><span class="sxs-lookup"><span data-stu-id="f36e7-148">After a few seconds, notice the new rule in the **Inbound security rules** blade.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="f36e7-150">Modifier une règle</span><span class="sxs-lookup"><span data-stu-id="f36e7-150">Change a rule</span></span>
<span data-ttu-id="f36e7-151">Pour modifier la règle créée précédemment pour autoriser le trafic entrant en provenance d’**Internet** uniquement, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-151">To change the rule created above to allow inbound traffic from the **Internet** only, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-152">Dans le panneau **Groupes de sécurité réseau** ou le panneau **Ressources** présenté ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-152">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="f36e7-153">Sous l’onglet **Paramètres** , cliquez sur la règle créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="f36e7-153">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="f36e7-154">Dans le panneau **allow-https**, modifiez la propriété **Source** comme indiqué ci-dessous, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-154">In the **allow-https** blade, change the **Source** property as shown below, and then click **Save**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="f36e7-156">Supprimer une règle</span><span class="sxs-lookup"><span data-stu-id="f36e7-156">Delete a rule</span></span>

<span data-ttu-id="f36e7-157">Pour supprimer la règle créée précédemment, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-157">To delete the rule created above, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-158">Dans le panneau **Groupes de sécurité réseau** ou le panneau **Ressources** présenté ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-158">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="f36e7-159">Sous l’onglet **Paramètres** , cliquez sur la règle créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="f36e7-159">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="f36e7-160">Dans le panneau **allow-https**, cliquez sur **Supprimer**, puis sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-160">In the **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="f36e7-162">Gérer les associations</span><span class="sxs-lookup"><span data-stu-id="f36e7-162">Manage associations</span></span>
<span data-ttu-id="f36e7-163">Vous pouvez associer un groupe de sécurité réseau à des cartes réseau et des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="f36e7-163">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="f36e7-164">Vous pouvez également dissocier un groupe de sécurité réseau de n’importe quelle ressource à laquelle il est associé.</span><span class="sxs-lookup"><span data-stu-id="f36e7-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="f36e7-165">Associer un groupe de sécurité réseau à une carte réseau</span><span class="sxs-lookup"><span data-stu-id="f36e7-165">Associate an NSG to a NIC</span></span>
<span data-ttu-id="f36e7-166">Pour associer le groupe de sécurité réseau **NSG-FrontEnd** à la carte réseau **TestNICWeb1**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-166">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-167">Dans le panneau **Groupes de sécurité réseau** ou le panneau **Ressources** présenté ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-167">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="f36e7-168">Sous l’onglet **Paramètres**, cliquez sur **Interfaces réseau** > **Associer** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-168">In the **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="f36e7-170">Dissocier un groupe de sécurité réseau d’une carte réseau</span><span class="sxs-lookup"><span data-stu-id="f36e7-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="f36e7-171">Pour dissocier le groupe de sécurité réseau **NSG-FrontEnd** de la carte réseau **TestNICWeb1**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-171">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-172">Dans le portail Azure, cliquez sur **Groupes de ressources >** > **RG-NSG** > **...** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-172">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="f36e7-173">Dans le panneau **TestNICWeb1**, cliquez sur **Modifier la sécurité...** > **Aucune**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-173">In the **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="f36e7-175">Vous pouvez également utiliser ce panneau pour associer la carte réseau à n’importe quel groupe de sécurité réseau existant.</span><span class="sxs-lookup"><span data-stu-id="f36e7-175">You can also use this blade to associate the NIC to any existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="f36e7-176">Dissocier un groupe de sécurité réseau d’un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="f36e7-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="f36e7-177">Pour dissocier le groupe de sécurité réseau **NSG-FrontEnd** du sous-réseau **FrontEnd**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-177">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-178">Dans le portail Azure, cliquez sur **Groupes de ressources >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-178">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="f36e7-179">Dans le panneau **Paramètres**, cliquez sur **Sous-réseaux** > **FrontEnd** > **Groupe de sécurité réseau** > **Aucun**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-179">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="f36e7-181">Dans le panneau **FrontEnd**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-181">In the **FrontEnd** blade, click **Save**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="f36e7-183">Association d’un groupe de sécurité réseau à un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="f36e7-183">Associate an NSG to a subnet</span></span>

<span data-ttu-id="f36e7-184">Pour associer à nouveau le groupe de sécurité réseau **NSG-FrontEnd** au sous-réseau **FrontEnd**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-184">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="f36e7-185">Dans le portail Azure, cliquez sur **Groupes de ressources >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-185">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="f36e7-186">Dans le panneau **Paramètres**, cliquez sur **Sous-réseaux** > **FrontEnd** > **Groupe de sécurité réseau** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-186">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="f36e7-187">Dans le panneau **FrontEnd**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-187">In the **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="f36e7-188">Vous pouvez également associer un groupe de sécurité réseau à un sous-réseau à partir du panneau **Paramètres** du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f36e7-188">You can also associate an NSG to a subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="f36e7-189">Suppression d'un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="f36e7-189">Delete an NSG</span></span>
<span data-ttu-id="f36e7-190">Vous ne pouvez supprimer un groupe de sécurité réseau que s’il n’est associé à aucune ressource.</span><span class="sxs-lookup"><span data-stu-id="f36e7-190">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="f36e7-191">Pour supprimer un groupe de sécurité réseau, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f36e7-191">To delete an NSG, complete the following steps:.</span></span>

1. <span data-ttu-id="f36e7-192">Dans le portail Azure, cliquez sur **Groupes de ressources >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-192">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="f36e7-193">Dans le panneau **Paramètres**, cliquez sur **Interfaces réseau**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-193">In the **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="f36e7-194">Si des cartes réseau sont répertoriées, cliquez sur la carte réseau et suivez l’étape 2 de [Dissocier un groupe de sécurité réseau d’une carte réseau](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="f36e7-194">If there are any NICs listed, click the NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="f36e7-195">Répétez l’étape 3 pour chaque carte réseau.</span><span class="sxs-lookup"><span data-stu-id="f36e7-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="f36e7-196">Dans le panneau **Paramètres**, cliquez sur **Sous-réseaux**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-196">In the **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="f36e7-197">Si des sous-réseaux sont répertoriés, cliquez sur le sous-réseau et suivez les étapes 2 et 3 de [Dissocier un groupe de sécurité réseau d’un sous-réseau](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="f36e7-197">If there are any subnets listed, click the subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="f36e7-198">Faites défiler à gauche vers le panneau **NSG-FrontEnd**, puis cliquez sur **Supprimer** > **Oui**.</span><span class="sxs-lookup"><span data-stu-id="f36e7-198">Scrolls left to the **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="f36e7-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f36e7-200">Next steps</span></span>
* <span data-ttu-id="f36e7-201">[Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f36e7-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
